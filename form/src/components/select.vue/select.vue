<template>
    <div>
      <div class="dropdown">
        <button class="form__button">Значения</button>
        <div id="myDropdown" class="dropdown-content">
          <li v-for="option in options" :key="option">
            <label :for="`option_${option}`">{{ option }}</label>
            <input type="checkbox" :id="`option_${option}`" :value="option" v-model="selectedOptions" />
          </li>
        </div>
      </div>
      <!-- <p>Selected Options: {{ selectedOptions }}</p> -->
    </div>
  </template>

<script>
export default {
    name: "MultiSelector",
    data() {
        return {
            options: ['VIP', 'Проблемные', 'ОМС'],
            selectedOptions: [],
        };
    },
    // methods: {
    //     toggleAll() {
    //         if (this.areAllOptionsSelected()) {
    //             this.selectedOptions = [];
    //         } else {
    //             this.selectedOptions = [...this.options];
    //         }
    //     },
    //     areAllOptionsSelected() {
    //         return this.options.length > 0 && this.options.every((option) => this.selectedOptions.includes(option));
    //     },
    // },
};
</script>

<style scoped>
.multi-selector {
    border: 1px solid #fc0000;
    padding: 15px;
}

ul {
    /* list-style-type: none; */
    padding: 0;
    display: flex;
    flex-wrap: wrap;
    /* margin: 0; */
    margin: 40px;
}

li {
    /* margin-left: 10px;
    margin-bottom: 5px; */
    padding: 5px;
    list-style-type: none;
}


.dropdown-content {
    display: none;
    position: absolute;
    background-color: #ffffff;
    min-width: 150px;
    box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
    z-index: 1;
}



.dropdown-content a:hover {
    background-color: #f1f1f1;
}


.dropdown:hover .dropdown-content {
    display: block;
}

</style>