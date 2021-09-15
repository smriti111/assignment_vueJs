<template>
  <div id="app">
    <TabNav
      :tabs="['Thirds', 'Fifths', 'Magic']"
      :selected="selected"
      @selected="setSelected"
    >
      <Tab :isSelected="selected === 'Thirds'">
        <Thirds :tasks="thirds"/>
      </Tab>
      <Tab :isSelected="selected === 'Fifths'">
        <Fifths :tasks="fifths"/>
      </Tab>
      <Tab :isSelected="selected === 'Magic'">
        <Magic :tasks="magic"/>
      </Tab>
    </TabNav>
  </div>
</template>
<script>
import Vue from 'vue/dist/vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(VueAxios,axios);


import TabNav from "./components/TabNav.vue";
import Tab from "./components/Tab.vue";
import Table from "./components/Table.vue";
import Thirds from "./components/Thirds.vue";
import Fifths from "./components/Fifths.vue";
import Magic from "./components/Magic.vue";

export default {
  name: "App",
  components: { TabNav, Tab, Table, Thirds, Fifths, Magic },
  data() {
    return {
      selected: "Thirds",
      tasks:[],
      fifths:[],
      thirds:[],
      magic:[],
    };
  },
  methods: {
    setSelected(tab) {
      this.selected = tab;
    },
  },

  mounted(){
    Vue.axios.get('https://jsonplaceholder.typicode.com/posts')
    .then((resp)=>{
      this.tasks=resp.data;
      //console.warn(resp.data);
      //console.log(this.tasks)

      for (let i = 0; i < this.tasks.length; i++) {
      if (this.tasks[i].id % 3 == 0) {
        this.thirds.push(this.tasks[i]);
      }
      if (this.tasks[i].id % 5 == 0) {
        this.fifths.push(this.tasks[i]);
      }
      if (this.tasks[i].id % 5 == 0 && this.tasks[i].id % 3 == 0) {
        this.magic.push(this.tasks[i]);
      }
    }
    console.log(this.magic);
    })
      
    
    

  }
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
  margin-left: 20px;
  margin-bottom: 20px;
  /* display: flex; */
  flex-direction: row;
  /* justify-content: center; */
}
</style>