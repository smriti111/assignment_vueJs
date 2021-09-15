<template>
  <div class="container">
      
    <input class="search"
      type="text"
      placeholder="Filter by title or body"
      v-model="filter"
    />
    <i @click="reset_value()" class="refresh fas fa-sync-alt"></i>
    <table class="table table-striped table-bordered">
      <thead>
        <tr>
          <!-- <th>Sr.</th> -->
          <th>ID</th>
          <th>Title</th>
          <th>Body</th>
        </tr>
      </thead>
      <tbody>
        <tr :key="item.id" v-for="(item, index) in filteredRows">
          <td>{{item.id}}</td>
          <td v-html="highlightMatches(item.title)"></td>
          <td v-html="highlightMatches(item.body)"></td>
          <!-- <td >{{ item.title }}</td>
          <td >{{ item.body }}</td>
       -->
          <td><i @click="onDelete(index)" class="delete fas fa-trash"></i></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    tasks: Array,
  },
  data(){
      return{
          filter:'',
          query:'',
          reset:[],
          //reset:this.tasks,
      }
  },
  methods: {
    onDelete(index) {
      console.log(index);
      this.tasks.splice(index, 1);
      console.log("inside delete")
      console.log(this.reset)
    },

    highlightMatches(text) {
      const matchExists = text.toLowerCase().includes(this.filter.toLowerCase());
      if (!matchExists) return text;

      const re = new RegExp(this.filter, "ig");
      return text.replace(
        re,
        (matchedText) => `<strong>${matchedText}</strong>`
      );
    },
    
    reset_value(){
        window.location.reload()
    }
  },

  beforeMount(){
      this.reset=this.tasks;
  },

 computed: {
  filteredRows() {
    return this.tasks.filter(row => {
      const title = row.title.toString().toLowerCase();
      const body = row.body.toLowerCase();
      const searchTerm = this.filter.toLowerCase();

      return title.includes(searchTerm) ||
        body.includes(searchTerm);
    });
  }
},
};
</script>

<style scoped>
.search{
    margin-top: 20px;
    margin-bottom: 20px;
    width:31%;
    padding: 10px;
}
.delete {
  color: rosybrown;
}
.refresh{
    color: green;
    padding: 10px;
}
td:hover {
  background-color: beige;
}
</style>