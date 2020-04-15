<template>
<div>
    <Header/>

    <Uppload/>

    <div id="navbar">
        <!-- Latest Snippet-->
        <button v-on:click="LatestBtn">Latest</button>
        <button v-on:click="BestBtn">Best Snippet</button>
        <button v-on:click="ReportedBtn">Reported Snippet</button>
        
        
         <br>
    </div>
    <div id="error" v-if="ErrorOccured">
       <p>Error is occured,try again later</p>
    </div>
    <div id="loading" v-else>
      <div v-if="loading">Loading</div>
      
         <div v-else id="contain" v-for="Snippet in ApiData" v-bind:key="Snippet.id">
                  <h2 id="title"> Title:{{ Snippet.title}}</h2>         
                  <p id="content"> Content:{{ Snippet.content}}</p>
                  <p id="upload"> UploadDate:{{ Snippet.upload_dt}}</p>
                  <p id="score"> Score:{{ Snippet.score}}</p>
                  <p id="reported"> Reported:{{ Snippet.is_reported}}</p>
                  <button v-on:click="deleteBtn(Snippet.id)">Delete</button>
                  <button v-on:click="upVote(Snippet.id)">Upvote</button>
                  <button v-on:click="downVote(Snippet.id)">Downvote</button>
                  <button v-on:click="report(Snippet.id)">Report</button>
                  <button v-on:click="unreport(Snippet.id)">UnReport</button>
                
      </div>
    </div>
  <Footer/>
</div>
   
</template>
<script>
import axios from 'axios';
import Uppload from './Uppload';
import Header from './Header';
import Footer from './Footer';


export default {
  name:"ViewSnippet",
  components: {
    Uppload,Header,Footer
  },
  

  data () {
    return {
      ApiData: null,
       loading: false,
      ErrorOccured: false,
       title:"", 
       content:"",
       Added:false
      

      
    }
  },
  methods:{
     
      unreport(id){
            this.loading=true,
         axios
        .post('https://www.forverkliga.se/JavaScript/api/api-snippets.php?',{unreport:'',id: id})
        .then(response => {console.log(response.data)
                if(response !== null){
                    this.LatestBtn();
          }  }) 
        .catch(error => {
        console.log(error)
        this.errored = true
      })
      
      .finally(() => this.loading = false)
      },


    report(id){
          this.loading=true,
         axios
        .post('https://www.forverkliga.se/JavaScript/api/api-snippets.php?',{report:'',id: id})
        .then(response => {console.log(response.data)
                if(response !== null){
                    this.LatestBtn();
          }  }) 
        .catch(error => {
        console.log(error)
        this.errored = true
      })
      
      .finally(() => this.loading = false)
    },


  downVote(id){
       this.loading=true,
         axios
        .post('https://www.forverkliga.se/JavaScript/api/api-snippets.php?',{downvote:'',id: id})
        .then(response => {console.log(response.data)
                if(response !== null){
                    this.LatestBtn();
          }  }) 
        .catch(error => {
        console.log(error)
        this.errored = true
      })
      
      .finally(() => this.loading = false)
  },


     upVote(id){
         this.loading=true,
         axios
        .post('https://www.forverkliga.se/JavaScript/api/api-snippets.php?',{upvote:'',id: id})
        .then(response => {console.log(response.data)
                if(response !== null){
                    this.LatestBtn();
          }  }) 
        .catch(error => {
        console.log(error)
        this.errored = true
      })
      
      .finally(() => this.loading = false)
   },

   deleteBtn(id){
       axios
      .post('https://www.forverkliga.se/JavaScript/api/api-snippets.php?',{delete:'',id: id})
      .then(response => {(this.ApiData = response.data)
      if(response!==null){
        this.LatestBtn();
      }
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
   },


   LatestBtn() {
     this.loading=true,
     
    axios
      .get('https://www.forverkliga.se/JavaScript/api/api-snippets.php?latest')
      .then(response => (this.ApiData = response.data))
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  
  },
   BestBtn() {
     this.loading=true,
    
    axios
      .get('https://www.forverkliga.se/JavaScript/api/api-snippets.php?best')
      .then(response => (this.ApiData = response.data))
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  
  },
   ReportedBtn() {
     this.loading=true,
     
    axios
      .get('https://www.forverkliga.se/JavaScript/api/api-snippets.php?reported')
      .then(response => (this.ApiData = response.data))
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  
  },

  }

}
</script>
<style>
#navbar{
  background-color: brown;
  padding: 20px;

}
#loading{
  background-color: rgb(159, 198, 241);
  padding: 20px;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  
}
#contain{
border:5px solid cadetblue;

}
#title{
 padding:10px;
 background: cadetblue;
 
}
</style>