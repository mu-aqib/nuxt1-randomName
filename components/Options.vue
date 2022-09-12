<script lang="ts" setup>
    import {
        Gender,
        Popularity,
        Length
    } from '@/data'

    interface validOptions {
        options: {
            gender: Gender,
            popularity: Popularity,
            length: Length
        },
        singleOption: {
            title: String,
            category: string,
            buttons: Gender[] | Popularity[] | Length[]
        }
    }

    // define interface to validate props with typescript.
    let props = defineProps < validOptions > ();
    
    const computeButtonClasses = (value, index) => {
        let classes = ''
        if(props.options[props.singleOption.category] === value) {
            // console.log(true)
            classes = 'option-active';
        }
        else{
            // console.log(false)
        }
        if(index === 0)  classes += ' option-left'
        if(index === props.singleOption.buttons.length - 1) classes += ' option-right'
        return classes;
    };

</script>

<template>

    <div class="option-container">
        <h4> {{singleOption.title}} </h4>

        <div class="option-buttons">
            <button class="option" 
                v-for="(value, index) in singleOption.buttons" :key="value"

                :class="computeButtonClasses(value, index)"

                @click="options[singleOption.category] = value"
            >
                {{value}}
            </button>
        </div>

    </div>

</template>
