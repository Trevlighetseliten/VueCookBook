<template>
    <div class="stepper-wrapper">
        <ul :class="['default-stepper', stepperClass]">
            <li v-for="(step, index) in steps" 
                :key="step.value"
                :class="[{ active: step.done === true },'default-stepper-item', stepperItemClass]"
                :style="stepWidthStyle"
                @click="onStepPressed(step.value, index)">
                {{ stepTitle(step) }}
            </li>
            
        </ul>
    </div>
</template>

<script>
    export default {
        props:{
            steps: {
                type: Array,
                required: true
            },
            showTitle: {
                type: Boolean,
                required: false,
                default: false
            },
            stepperClass:{
                type: String,
                required: false,
            },
            stepperItemClass:{
                type: String,
                required: false,
            }
        },
        computed: {
            stepWidthStyle: function(){
                let widthRate = (this.steps === null || this.steps === undefined || this.steps.length === 0)
                    ? 0 
                    : 1 / this.steps.length * 100;
                return 'width: ' + widthRate + '%';
            }
        },
        methods: {
            stepTitle: function(step){
                return this.showTitle
                    ? step.title
                    : '';
            },
            onStepPressed: function(stepValue, index){
                this.$emit('stepPressed', stepValue, index);
            }
        }
    }
</script>

<style scoped>
    .stepper-wrapper {
        z-index: 1;
        display: inline-flex;
        white-space: nowrap;
        min-width:105px;
    }
    
    .default-stepper {
        width: 100%;
        list-style-type: none;
        text-align: center;
        padding: 0px;
        margin: 0px;
    }

    .default-stepper-item {
        float: left;
        width: 0%;
        position: relative;
        text-align: center;
        cursor: pointer;
    }

    .default-stepper-item:before {
        content: " ";
        line-height: 30px;
        border-radius: 50%;
        width: 20px;
        height: 20px;
        border: 1px solid #ccc;
        display:block;
        text-align: center;
        margin: 0 auto 10px;
        background-color: white;
        z-index:1;
    }

    .default-stepper-item:after {
        content: "";
        position: absolute;
        width: 100%;
        height: 5px;
        border: 1px solid #ccc;
        background-color: #ddd;
        top: 8px;
        left: -50%;
        z-index: -1;
    }

    .default-stepper-item:first-child:after {
        content: none;
    }

    .default-stepper-item.active {
        color: dodgerblue;
    }

    .default-stepper-item.active:before {
        border-color: dodgerblue;
        background-color: dodgerblue
    }

    .default-stepper-item.active:after {
        background-color: dodgerblue;
        border-color: dodgerblue;
    }
</style>