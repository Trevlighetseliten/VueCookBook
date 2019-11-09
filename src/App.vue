<template>
  <div id="app">
    <div style="padding: 40px 40px;">
      <h1>Vue Cookbook</h1>
      <p>A collection of components created with Vue 3 and bootstrap 4</p>
    </div>
    <tab-panel :tabItems="tabs" @tabChanged="changeTab"></tab-panel>
    <div class="tab-content">
      <div v-if="selectedTab === 10">
        <tab-bar-section></tab-bar-section>
      </div>
      <div v-if="selectedTab === 20">
        <div class="card" style="padding: 30px 50px; min-width:205px;">
          <stepper :steps="steps" :showTitle="true" :stepperItemClass="'my-stepper-item'" @stepPressed="onStepPressed"></stepper>
        </div>
        <div style="margin-top: 50px">
          <button class="btn btn-primary" style="margin-right: 20px;" @click="increment">Increment</button>
          <button class="btn btn-secondary" @click="decrement">Decrement</button>
        </div>
      </div>
      <div v-if="selectedTab === 30">
        <checkbox-selection-tree-section></checkbox-selection-tree-section>
      </div>
      <div v-if="selectedTab === 40">
        <responsive-tab-panel></responsive-tab-panel>
      </div>
    </div>
  </div>
</template>

<script>
import TabPanel from './components/tab-panel.vue'
import Stepper from './components/stepper.vue'
import TabBarSection from './examples/tab-bar-section.vue'
import CheckboxSelectionTreeSection from './examples/checkbox-selection-tree-section.vue';
import ResponsiveTabPanel from './components/responsive-tab-panel.vue';

export default {
  name: 'app',
  components: {
    TabPanel,
    Stepper,
    TabBarSection,
    CheckboxSelectionTreeSection,
    ResponsiveTabPanel
  },
  data: function(){
    return {
      selectedTab: 10,
      tabs: [
        { value: 10, title: "Tab bar" },
        { value: 20, title: "Stepper" },
        { value: 30, title: "Checkbox selection tree" },
        { value: 40, title: "Tab 3" },
      ],
      steps: [
        { value: 1, title: "Prepare", done: true },
        { value: 2, title: "Execute", done: true},
        { value: 3, title: "Reflect", done: false },
        { value: 4, title: "Post-executed", done: false }
      ],
      tabItemUsage: '<tab-panel :tabItems="tabs" @tabChanged="changeTab"></tab-panel>'
    }
  },
  methods:{
    changeTab: function(value){
      /*eslint no-console: off*/
      console.log(value);
      this.selectedTab = value;
    },
    onStepPressed: function(value, index){
      for(let i = 0; i < this.steps.length; i++){
        this.steps[i].done = i <= index;
      }
    },
    increment: function(){
      var next = this.nextIndex();
      if(next > 0 && next < this.steps.length){
        this.steps[next].done = true;
      }
    },
    decrement: function(){
      var next = this.nextIndex();
      if(next === -1 ){
        this.steps[this.steps.length-1].done = false;
      }
      else if(next-1 > 0){
        this.steps[next-1].done = false;
      }
    },
    nextIndex: function(){
      return this.steps.findIndex((step) => {
        return step.done === false;
      });
    }
  }
}
</script>

<style scoped>
  .tab-content{
    margin: 50px 65px !important;
    text-align: left;
  }
</style>

<style>
#app {
  font-family: 'Roboto', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.container {
  padding: 2px 16px;
}

p.info-text {
  font-size:12px;
  margin: 0;
}

p.info-header {
  font-size: 18px;
  margin-bottom: 8px;
}

pre {
  overflow: hidden !important;
  background-color: #eee;
  padding: 6px 6px 12px 6px;
}

pre:hover {
  overflow:overlay !important;
}

pre code {
  font-size: 12px !important;
}

::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px grey; 
  border-radius: 10px;
}
 
/* Handle */
::-webkit-scrollbar-thumb {
  background: rgb(30, 144, 255); 
  border-radius: 10px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: rgb(21, 100, 179); 
}

.horizontal-scroll::-webkit-scrollbar{
  width: 7px !important;
}
/* .my-stepper-item.active {
    color: #25fb00 !important;
}

.my-stepper-item.active:before {
    border-color: #25fb00 !important;
    background-color: #25fb00 !important;
}

.my-stepper-item.active:after {
    background-color: #25fb00 !important;
    border-color: #25fb00 !important;
} */



/* .my-tabs {
  text-align: left
}

.my-tab-item {
  padding: 20px;
  margin: 100px;
  cursor:pointer;
  font-size: 40px;
}

.my-tab-item:hover {
  border-bottom: 5px solid yellow;
}

.my-tab-item.active {
  border-bottom: 5px solid purple;
} */


</style>
