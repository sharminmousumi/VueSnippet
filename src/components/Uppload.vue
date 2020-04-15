<template>
    <div id="form">
        <form v-on:submit="submitBtn" action="#" method="post">
      <label> Title:</label>
      <input id="titleForm" v-model="title" placeholder="Title">
      <br>
      <label>Content:</label>
      <input id="contentForm" v-model="content"  placeholder="Content">
      <br>
      <button id="submitbtn" type='submit'>Submit</button><h2 v-if="Added">Added snippet to the list!</h2>
    </form>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    name:'Uppload',

    data () {
    return {

       title:"", 
       content:"",
       Added:false
    }
      
    },

    methods:{
        submitBtn(event){  
       event.preventDefault();
       
       this.Added="";
         axios
        .post('https://www.forverkliga.se/JavaScript/api/api-snippets.php?',{add:'',title:this.title,content:this.content})
        .then(response => {(response.data)
          if(response !==null){
        this.Added=true;
          }
        }) 
        .catch(error => {
        console.log(error)
        this.errored = true
      })
      
        }
        
    }
    
    
}
</script>
<style>
#titleForm{
 width: 30%;
  padding-right:20px;
  padding-bottom:5px;
  display: inline-block;
  border: 1px solid burlywood;
  border-radius: 4px;
  box-sizing: border-box;
  margin-left:25px;
}
#contentForm{
    width: 30%;
  padding-right:30px;
  padding-bottom:20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid burlywood;
  border-radius: 4px;
  box-sizing: border-box;
   }
   #submitbtn{
       width: 10%;
  background-color: #4CAF50;
  color: white;
  padding: 7px 10px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
   }
   #form{
  border-radius: 5px;
  background-color: cadetblue;
  padding: 20px;
  margin-top:-7px;
 
   }

</style>