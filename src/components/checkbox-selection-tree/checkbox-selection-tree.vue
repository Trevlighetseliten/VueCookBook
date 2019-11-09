<template>
    <div>
        <div v-for="(selectionTree,index) in selectionTreeModel" :key="index" :class="{indented: indent}">
            <hierarchical-checkbox v-model="selectionTreeModel[index]"></hierarchical-checkbox>
            <div v-if="!isLeaf(selectionTreeModel[index]) && selectionTreeModel[index].expanded">
                <checkbox-selection-tree :selection-tree-model="selectionTreeModel[index].children" :indent="true"></checkbox-selection-tree>
            </div>
        </div>
        
    </div>
</template>

<script>
    import HierarchicalCheckbox from './hierarchical-checkbox.vue';

    export default {
        name: "checkbox-selection-tree",
        components:{
            HierarchicalCheckbox
        },
        props: {
            selectionTreeModel: {
                type: Array,
                required: true
            },
            indent: {
                type: Boolean,
                required: false,
                default: false
            }
        },
        methods: {
            isLeaf: function(selectionTree){
                return selectionTree.children === undefined || selectionTree.children === null || selectionTree.children.length <= 0;
            }
        }
    }
</script>

<style scoped>
    .indented {
        margin-left: 40px;
    }
</style>