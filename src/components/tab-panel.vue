<template>
    <div class="tabs">
        <ul :class="tabContainerClass">
            <li v-for="tab in tabItems"
                :key="tab.value" 
                :class="[tabItemClass, {active: isActiveTab(tab.value)}]"
                @click="onChangeTab(tab)">{{tab.title}}</li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        tabItems: {
            type: Array,
            required: true
        },
        tabContainerClass: {
            type: String,
            required: false,
            default: 'default-tab-container'
        },
        tabItemClass: {
            type: String,
            required: false,
            default: 'default-tab-item'
        },
    },
    data: function(){
        return {
            selectedTabValue: (this.tabItems !== null && this.tabItems !== undefined && this.tabItems.length > 0)
                ? this.tabItems[0].value
                : ''
        }
    },
    methods: {
        isActiveTab: function(tabValue){
            return this.selectedTabValue === tabValue;
        },
        onChangeTab: function(tab){
            this.selectedTabValue = tab.value;
            this.$emit("tabChanged", tab.value);
        },
    }
}

</script>

<style scoped>
    .tabs ul {
        list-style: none;
        display: flex;
        flex-wrap: wrap;
        -ms-flex-wrap: wrap;
    }

    .tabs li {
        display: inline;
    }

    .default-tab-container {
        text-align: left;
    }

    .default-tab-item{
        padding: 10px 20px;
        margin: 0 5px;
        cursor: pointer;
    }

    .default-tab-item:hover{
         border-bottom: 2px solid rgba(0,0,0,0.1)
    }

    .default-tab-item.active {
        border-bottom: 2px solid black;
    }
</style>

