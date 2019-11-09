<template>
    <div>
        <checkbox-selection-tree :selection-tree-model="selectionTreeModel"></checkbox-selection-tree>
    </div>
</template>

<script>
    import CheckboxSelectionTree from '../components/checkbox-selection-tree/checkbox-selection-tree.vue';

    export default {
        components: {
            CheckboxSelectionTree
        },
        data: function(){
            return {
                selectionTreeModel:[
                    { value: 1, title: "Root 1", selected: true, expanded: false, children: [
                      {value: 11, title: "Node 1", selected: true, expanded: false, children: [
                          {value: 111, title: "Leaf 1", selected: false, expanded: false },
                          {value: 112, title: "Leaf 2", selected: true, expanded: false },
                      ]}  
                    ]},
                    { value: 2, title: "Root 2", selected: false, expanded: false, children: [
                        {value: 21, title: "Leaf 2", selected: false, expanded: false}
                    ]},
                    { value: 3, title: "Root 3", selected: false, expanded: false},
                ]
            }
        }
    }
</script>

<style scoped>

</style>