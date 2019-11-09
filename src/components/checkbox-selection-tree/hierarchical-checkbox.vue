<template>
    <div>
        <div class="checkbox-tree-item">
            <div class="checkbox-icon-container">
                <div v-if="isExpandible">
                    <i v-if="value.expanded" class="fa fa-minus-circle" @click="onExpandClicked"></i>
                    <i v-else class="fa fa-plus-circle" @click="onExpandClicked"></i>
                </div>
            </div>
            <div class="checkbox-container"><input type="checkbox" class="form-check-input" :indeterminate.prop="isIndeterminate" :value="value.selected" :checked="value.selected" @input="selectionChanged">{{ value.title }}</div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        value: {
            type: Object,
            required: true
        }
    },
    computed: {
        isExpandible: function(){
            return !this.isLeaf(this.value);
        },
        isIndeterminate: function() {
            if(this.isLeaf(this.value)) return false;
            return this.nodeInDeterminate(this.value);
        },
        children: function() {
            return this.value.children;
        }
    },
    watch: {
        children: function(newChildrenValue) {
            let anySelected = newChildrenValue.some((child) => { return child.selected});
            this.$emit('input', Object.assign(this.value, { selected: anySelected}));
        }
    },
    methods: {
        selectionChanged: function(event){
            let value = event.target.checked;
            this.value.selected = value;
            if(this.isExpandible){
                this.value.children.forEach((node) => {
                    console.log("propagates")
                    this.propagateSelection(node, value);
                })
            }

            this.$emit('input', this.value );
        },
        onExpandClicked: function(){
            this.$emit('input', Object.assign(this.value, { expanded: !this.value.expanded}))
        },
        propagateSelection(node, selectionValue){
            node.selected = selectionValue;
            if(node.children !== undefined && node.children !== null && node.children.length > 0){
                console.log("propagating node " + node.value);
                node.children.forEach(element => {
                    console.log("propagating node " + element.value);
                    this.propagateSelection(element, selectionValue);
                });
            }

        },
        isLeaf(node){
            return node.children === undefined || node.children === null || node.children <= 0;
        },
        nodeInDeterminate: function(node){
            let isIndeterminate = node.children.some((child) => {
                       return child.selected;
                   }) &&
                   !node.children.every((child) => {
                       return child.selected
                   });

            node.children.forEach((childNode) => {
                if(!this.isLeaf(childNode)){
                    isIndeterminate = isIndeterminate || this.nodeInDeterminate(childNode);
                }
            })
            return isIndeterminate;
        }
    }
}
</script>

<style scoped>
    .checkbox-tree-item {
        display:flex;
        flex-direction: row;
        display:inline-flex;
        white-space: nowrap;
    }

    .checkbox-icon-container {
        margin-top: 1.8px;
        margin-right:10px; 
        width: 30px;
        font-size:12px;
    }

    .checkbox-container {
        padding-right: 0;
        line-height:20px;
    }
</style>