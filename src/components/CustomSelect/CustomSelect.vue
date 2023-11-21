<template>
    <div class="custom-select" ref="customSelect">
        <div class="selected-value placeholder" :class="{ active: isDropdownVisible }" @click="toggleDropdown">
            {{ selectedOption ? selectedOption.title : placeholder }}
        </div>
        <img :class="{ flipped: isDropdownVisible }" class="arrow" src="../../assets/arrowSelect.svg" alt="Arrow"
            @click="toggleDropdown">
        <transition name="fade">
            <ul v-if="isDropdownVisible" class="options-list">
                <li v-for="option in options" :key="option.id" @click="selectOption(option)">
                    {{ option.title }}
                </li>
            </ul>
        </transition>
    </div>
</template>
  
<script>
export default {
    name: 'CustomSelect',
    props: {
        options: {
            type: Array,
            require: true,
        },

        selectedValue: {
            type: Object,
            default: null,
        },

        placeholder: {
            type: String,
            default: 'Выберите значение',
        },

        onChange: {
            type: Function,
            require: true,
        },
    },

    data() {
        return {
            isDropdownVisible: false,
            selectedOption: this.selectedValue,
        };
    },

    mounted() {
        document.addEventListener('click', this.handleClickOutside);
    },

    beforeUnmount() {
        document.removeEventListener('click', this.handleClickOutside);
    },

    methods: {
        toggleDropdown(event) {
            if (event.target.classList.contains('arrow') || event.target.classList.contains('selected-value')) {
                this.isDropdownVisible = !this.isDropdownVisible;
            }
        },

        selectOption(option) {
            this.selectedOption = option;
            this.onChange(option);
            this.isDropdownVisible = false;
        },

        handleClickOutside(event) {
            if (!this.$refs.customSelect.contains(event.target)) {
                this.isDropdownVisible = false;
            }
        },
    },
};
</script>
  
<style scoped>
.custom-select {
    position: relative;
    width: 400px;
    border: 2px solid #F968bf;
    color: #29277d;
    display: inline-block;
    cursor: pointer;
}

.selected-value {
    padding: 8px;
    color: rgba(41, 39, 125, 0.40);
}

.selected-value.active {
    background-color: #DADEFE;
}

.arrow[data-v-3960f36f] {
    top: 10px;
}

.arrow {
    position: absolute;
    top: 30%;
    right: 8px;
    fill: #5F88F4;
    transition: transform 0.3s ease-in-out;
}

.arrow.flipped {
    transform: translateY(-50%) rotate(180deg);
}

.options-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
    border: 2px solid #F968bf;
    border-top: none;
    overflow: hidden;
    transition: transform 0.3s ease-in-out;
}

.options-list li {
    padding: 8px;
    cursor: pointer;
}

.options-list li:hover {
    background-color: #DADEFE;
}
</style>
  