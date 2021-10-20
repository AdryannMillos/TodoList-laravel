<template>
<div class="toDoListContainer">
    <div class="heading">
        <h2 id="title">ToDo List</h2>
        <add-item-form v-on:reloadlist="getList()" />
    </div>
      <list-view :items="items" v-on:reloadlist="getList()"/>
</div>
</template>

<script>
import addItemForm from "./addItemForm.vue"
import listView from "./listView.vue"
export default {
    name: "app",
   data(){
       return{
           items:[ ]
       }

   },
    methods:{
        getList(){
            axios.get('api/items')
            .then(response=>{
                this.items = response.data
            })
            .catch(error => {
                console.log(error)
            })
        }
    },
    created(){
        this.getList()
    },
   components: {
       addItemForm,
       listView
   }
}

</script>

<style scoped>
.toDoListContainer{
    width: 350px;
    margin: auto;
}
.heading{
    background: #e6e6e6;
    padding: 10px;
}
#title{
    text-align: center;
}
</style>