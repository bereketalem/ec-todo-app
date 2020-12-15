<template>
  <div class="task">
      <h1>{{name}}</h1>

     <form @submit.prevent="addTask">

          <input type="text" placeholder="Enter a task to do.." v-model="taskName">       
      </form>
         <ul>
             <li v-for="(data,index) in Tasklist" 
                   v-bind:key="index">
                  {{data.taskName}}
              
                 <v-btn btn btn-default btn-lg v-on:click="remove">
                    <svg xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24">
                    <path d="M0 0h24v24H0z" fill="none"/><path d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM19 4h-3.5l-1-1h-5l-1 1H5v2h14V4z"/></svg>
                  </v-btn> 
              </li>
              
           </ul>
              <p id="error" v-if="warning">Lägg till todo</p> 
              <p v-if="show"><strong> Du har {{count}} todos att göra</strong></p>
                     
    </div>
</template>

<script>
export default {
  data() {
   return {
     name: 'TEFLON',
     taskName: '',
     Tasklist: [],
     show: false,
     warning: false,
     count:0
   }
  },

  methods: {
    addTask () {
      if (this.taskName == ''){
        this.warning = true;
      }else{
        this.count++;
        this.warning = false;
        this.show = true;
        this.Tasklist.push({taskName: this.taskName})
        this.taskName = '';
      }
    },
    remove(id){
      this.Tasklist.splice(id,1);
      if (id!=0) {
        this.count--;
      }
  }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/*@import "path/to/font-awesome/css/font-awesome.min.css";*/

.task {
  background: #fff;
   max-width: 30%;
   padding-left: 38%;
}
h1{
  text-align: center;
}
#error{
  padding: 0;
  color:red;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}

v-btn{
  float:right;
  color:red;
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}
ul li {
  padding: 20px;
  font-size: 1.3em;
  background-color: #E0EDf4;
  border-left: 5px solid #3EB3F6;
  margin-bottom: 2px;
  color: #3E5252;
  cursor: pointer;
  height: 25px;
}
p {
  text-align: center;
  padding:0;
  color: gray;
}
input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687F7F;
}

</style>
