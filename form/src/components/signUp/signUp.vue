<template>
        <div>
            <div v-for="(field, index) in fields" :key="index">
                <label class="form__label">{{ field.text }}</label>
                <inputPhone v-if="field.type === 'phoneNumber'" />
                <MultiselectCheckbox v-if="field.type === 'multiSelect'" class="form__input"
                    v-model="field.selectedOptions" :options="field.options" />
                <select v-if="field.type === 'select'" class="form__input form__select form__int">
                    <option v-for="option in field.options" :key="option" :value="option">{{ option }}</option>
                </select>
                <input v-if="field.type === 'checkbox'" type="checkbox" class="form__checkbox" />
                <input v-if="field.type === 'input'" class="form__input" type="text" v-model="field.value" />
                <p class="error" v-if="!field.value && submitted">{{ field.error }}
                </p>
            </div>
            <modal>
            <childComponent :submitted="submitted" :isValid="isValid" />
            <button class="form__btn" @click="submit" :disabled="!isValid">Зарегистрироваться</button>
        </modal>
        </div>
</template>


<script>

import { useVuelidate } from '@vuelidate/core';
import { required } from '@vuelidate/validators';
import { ref } from 'vue';
import MultiselectCheckbox from '../select.vue/select';
import inputPhone from '../number/numberVal'
import modal from '../window/windowBtn'

export default {
    components: { MultiselectCheckbox, inputPhone, modal },


    setup() {
        let fields = [
            { type: 'input', text: 'Фамилия', error: 'LastName is required', value: '' },
            { type: 'input', text: 'Имя', error: 'FirstName is required', value: '' },
            { type: 'input', text: 'Отчество', error: 'MiddleName is required', value: '' },
            { type: 'input', text: 'Дата рождения' },
            { type: 'phoneNumber', text: 'Номер телефона', phoneNumber: '', required: true },
            { type: 'select', text: 'Пол', options: ['Мужской', 'Женский'] },
            {
                type: 'multiSelect',
                text: 'Группа клиентов',
                options: []
            },
            {
                type: 'select',
                text: 'Лечащий врач',
                options: ['Иванов', 'Захаров', 'Чернышева'],
            },
            { type: 'checkbox', text: 'Не отправлять смс' },
            { type: 'input', text: 'Индекс' },
            { type: 'input', text: 'Страна' },
            { type: 'input', text: 'Область' },
            { type: 'input', text: 'Город', error: 'Город is required', value: '' },
            { type: 'input', text: 'Улица' },
            { type: 'input', text: 'Дом' },
            {
                type: 'input',
                text: 'Тип документа',
                options: ['Паспорт', 'Свидетельство о рождении', 'Вод. удостоверение']
            },
            { type: 'input', text: 'Серия' },
            { type: 'input', text: 'Номер' },
            { type: 'input', text: 'Кем выдан' },
            { type: 'input', text: 'Дата выдачи', error: 'Дата выдачи is required', value: '' },
        ];

        const rules = {
            fields: {
                required
            }
        };

        const v$ = useVuelidate(rules, { fields });

        const submitted = ref(false);

        function submit() {
            submitted.value = true;
        }

        const isValid = () => {
            v$.$touch();
            return !v$.$invalid;
        };

        return { v$, fields, submit, submitted, isValid };
    },
};
</script>
