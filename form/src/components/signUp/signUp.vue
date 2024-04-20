<template>
    <div>
        <div v-for="(field, index) in fields" :key="index">
            <label class="form__label">{{ field.text }}</label>
            <inputPhone v-if="field.number === true"/>
            <input v-if="!field.options" class="form__input" type="text" v-model="field.value" />
            <MultiselectCheckbox v-else-if="field.multiple === true" class="form__input" v-model="field.selectedOption"
                :options="field.options" />
            <select v-else class="form__input form__int" type="text" v-model="field.selectedOption">
                <option v-for="option in field.options" :key="option" :value="option">{{ option }}</option>
            </select>
            <p class="error" v-if="!field.value && submitted">{{ field.error }}
            </p>
        </div>
        <button class="form__btn" @click="submit" :disabled="!isValid">Submit</button>
    </div>
</template>


<script>

import { useVuelidate } from '@vuelidate/core';
import { required } from '@vuelidate/validators';
import { ref } from 'vue';
import MultiselectCheckbox from '../select.vue/select';
import inputPhone from '../number/numberVal'

export default {
    components: { MultiselectCheckbox, inputPhone },


    setup() {
        const fields = [
            { text: 'Фамилия', error: 'LastName is required', value: '' },
            { text: 'Имя', error: 'FirstName is required', value: '' },
            { text: 'Отчество', error: 'MiddleName is required', value: '' },
            { text: 'Дата рождения' },
            { text: 'Номер телефона', error: 'Phone Number is required', number: true, phoneNumberValue: '' },
            { text: 'Пол' },
            {
                text: 'Группа клиентов',
                options: [],
                multiple: true
            },
            {
                text: 'Лечащий врач',
                options: ['Иванов', 'Захаров', 'Чернышева'],
            },
            { text: 'Индекс' },
            { text: 'Страна' },
            { text: 'Область' },
            { text: 'Город', error: 'Город is required', value: '' },
            { text: 'Улица' },
            { text: 'Дом' },
            {
                text: 'Тип документа',
                options: ['Паспорт', 'Свидетельство о рождении', 'Вод. удостоверение']
            },
            { text: 'Серия' },
            { text: 'Номер' },
            { text: 'Кем выдан' },
            { text: 'Дата выдачи', error: 'Дата выдачи is required', value: '' },
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
