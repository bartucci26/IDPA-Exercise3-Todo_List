<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <add-item-form 
                v-on:reloadlist="getList()"
                />
        </div> <!--  :items - pass a prop called items with the items stored in the data array to list view  -->
        <list-view 
            :items="items"              
            v-on:reloadlist="getList()" /> 
    </div>
</template>

<script>
    
    import addItemForm from "./addItemForm"
    import listView from "./listView"
    export default {
        components: {
            addItemForm,
            listView
                
        },
        data: function() {
            return {
                items: []
            }

        },
        methods: {
            getList() {
                axios.get('api/items')
                .then(response =>{
                    this.items = response.data //if any data is fed, store in the array "items" above
                })
                .catch(error =>{
                    console.log(error);
                })
            }
        },
        created() {  //when this component is created, run getList method
            this.getList();
        }
    }
</script>

<style scoped >
.todoListContainer {
    width: 350px;
    margin: auto;
}
.heading {
    background: #e6e6e6;
    padding: 10px;
}

#title {
    text-align: center;
}
</style>