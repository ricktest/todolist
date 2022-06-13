<template>
   <header>
    <task-title></task-title>
  </header>
  <main>

    <div class="side">
      <AddToDolist @addItemHtml="addItemHtml" />
      <SelectStatus @statusChange="selectChange"/>
    </div>
    <div class="side">
      <ItemList @edit="edit" @updateStatus="updateStatus" @delitem="delitem" @handelStart="handelStart" @hadelChange="hadelChange" :items="items" :start="start" />
    </div>
    <div class="side">
      <ItemContent :todos="todos" @del="del" @addItem="addItem"/>
    </div>
  </main>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import TaskTitle from './components/TaskTitle.vue';
import AddToDolist from './components/AddToDolist.vue';
import SelectStatus from './components/SelectStatus.vue';
import ItemContent from './components/ItemContent/ItemContent.vue';
import ItemList from './components/ItemList/ItemList.vue';
export default {

  data() {  
      return {
        isAdd:null,
        todos:[],
        items:[],
        temp:[],
        count:0,
        start:0
      }
  },
  name: 'App',
  components: {
    TaskTitle,AddToDolist,SelectStatus,ItemContent,ItemList
  },
  methods: {

    addItemHtml(){
      this.count ++;
      this.todos.push({id: this.count,title:'',status:0});
    },

    del(){
      
      //this.todos.splice(index,1)
      
    },

    selectChange(selectValue){

        fetch('httP://192.168.88.143:5000/items?status='+selectValue, 
        {
          method: 'GET',
        })
        .then((res) => res.json())
        .then((data) => {
          
            if(data.status==='ok'){           
              this.items = data.toData;
            }
      });
      // console.log("123",selectValue,this.items);
    },
    delitem(id){
       fetch('httP://192.168.88.143:5000/deleteitem/'+id, 
            {
                method: 'DELETE',
            })
           
      
    },
    updateStatus(updataData){
        fetch('httP://192.168.88.143:5000/updatestatus/'+updataData.id, 
        {
            method: 'PUT',
        })
        .then((res) => res.json())
        .then((data) => {
           if(data.status==='ok'){
            let index = this.items.findIndex((el)=>el.id === updataData.id)
            this.items[index].status = data.toData.status
            console.log(this.items[index]);
           }
        });
    },
    addItem(itemData){

      let data ={
        title:itemData.title
      }

      fetch('httP://192.168.88.143:5000/additem', 
      {
          method: 'POST',
          body: JSON.stringify(data),
          headers: { 'content-type': 'application/json' },
      })
      .then((res) => res.json())
      .then((data) => {

          if(data.status==='ok'){
            //let index = this.todos.findIndex((el)=>el.id === itemData.id)
           
            //this.todos.splice(index,1)
            //console.log(index,this.todos);
            this.items.push(data.toData);
          }

      });
    },
    edit(updataData){
          let data ={
              title:updataData.title
          }
           console.log(data);
          //console.log(data);
          fetch('httP://192.168.88.143:5000/updateitem/'+updataData.id, 
          {
              method: 'PUT',
              body: JSON.stringify(data),
              headers: { 'content-type': 'application/json' },

          })
          .then((res) => res.json())
          .then((data) => {
              console.log(data);
          });
    },
    handelStart(index){
      this.start = index;
        //console.log(index);
    },
    hadelChange(changeData){
      //et tmep;
      //this.items[changeData]
      console.log(changeData);
    }

  },

  mounted(){

     fetch('httP://192.168.88.143:5000/items', 
      {
        method: 'GET',
      })
      .then((res) => res.json())
      .then((data) => {
        
          if(data.status==='ok'){
            this.items = data.toData;
            console.log(this.items);
          }
          
    });
  }
}
</script>


<style>

  header{
    width: 100%;
  }

  main{
    
    width: 100%;
  }

  .side{
    display: flex;
    width: 30%;
    margin: auto;
    justify-content: start;
    margin-top:20px;
  }
</style>