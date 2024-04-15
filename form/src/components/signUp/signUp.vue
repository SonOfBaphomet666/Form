<template>
    <div>
      <div v-for="(field, index) in fields" :key="index">
        <label class="form__label">{{ field.text }}</label>
        <input v-if="!field.options" class="form__input" type="text" v-model="field.value" />
        <!-- Replace select element with MultiselectCheckbox component -->
        <MultiselectCheckbox v-else-if="Array.isArray(field.options)" class="form__input" v-model="field.value" :options="field.options" :multiple="field.multiple" />
        <p class="error" v-if="!field.value && submitted">{{ field.error }}</p>
      </div>
      <button @click="submit" :disabled="!isValid">Submit</button>
    </div>
  </template>

<script>
import { useVuelidate } from '@vuelidate/core';
import { required } from '@vuelidate/validators';
import { ref } from 'vue';
import MultiselectCheckbox from '../select.vue/select'

export default {
    components: { MultiselectCheckbox },

    setup() {
        const fields = [
            { text: 'Фамилия', error: 'LastName is required', value: '' },
            { text: 'Имя', error: 'FirstName is required', value: '' },
            { text: 'Отчество', error: 'MiddleName is required', value: '' },
            { text: 'Дата рождения', },
            { text: 'Номер телефона', error: 'Number is required', value: '' },
            { text: 'Пол' },
            {
                text: 'Группа клиентов',
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
                text: "Тип документа",
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