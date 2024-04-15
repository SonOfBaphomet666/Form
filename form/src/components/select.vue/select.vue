<template>
    <div class="multi-selector">
        <label for="selectAll" :style="{ marginRight: '10px' }">Select All</label>
        <input type="checkbox" id="selectAll" @change="toggleAll()" />
        <div class="dropdown">
            <button class="dropbtn">Select Option</button>
            <div id="myDropdown" class="dropdown-content">
                <li v-for="(option, index) in options" :key="index">
                    <label :for="`option${index}`" :style="{ marginRight: '10px' }">{{ option }}</label>
                    <input type="checkbox" :id="`option${index}`" :value="option" v-model="selectedOptions" />
                </li>
            </div>
        </div>
        <p>Selected Options: {{ selectedOptions }}</p>
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
    methods: {
        toggleAll() {
            if (this.areAllOptionsSelected()) {
                this.selectedOptions = [];
            } else {
                this.selectedOptions = [...this.options];
            }
        },
        areAllOptionsSelected() {
            return this.options.length > 0 && this.options.every((option) => this.selectedOptions.includes(option));
        },
    },
};
</script>

<style scoped>
.multi-selector {
    border: 1px solid #ccc;
    padding: 15px;
}

ul {
    list-style-type: none;
    padding: 0;
    display: flex;
    flex-wrap: wrap;
    margin: 0;
}

li {
    margin-right: 10px;
    margin-bottom: 10px;
}

/* The dropdown container */
.dropdown {
    position: relative;
    display: inline-block;
}

/* Dropdown content (hidden by default) */
.dropdown-content {
    display: none;
    position: absolute;
    background-color: #f9f9f9;
    min-width: 160px;
    box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
    z-index: 1;
}

/* Links inside the dropdown */
.dropdown-content a {
    color: black;
    padding: 12px 16px;
    text-decoration: none;
    display: block;
}

/* Change color of dropdown links on hover */
.dropdown-content a:hover {
    background-color: #f1f1f1;
}

/* Show the dropdown menu on click */
.dropdown:hover .dropdown-content {
    display: block;
}

/* Other fun stuff */
.dropbtn {
    cursor: pointer;
    font-size: 14px;
    border: none;
    outline: none;
    color: blue;
    padding: 14px 16px;
    background-color: inherit;
    font-family: inherit;
    margin: 0;
}
</style>