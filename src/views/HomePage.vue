<script>
import { onMounted, VueElement } from 'vue';
import { ref } from 'vue'
import axios from 'axios'
export default {
  name: 'HomePage',
  async setup(){
            let tweets = ref([])
            let username = localStorage.getItem("username");
            let accesstoken = localStorage.getItem("userId");
            

         //   await axios.get('https://localhost:7189/api/Timeline?userId=48e9baa7-62cb-4f97-a840-8c1c1c9738ec').then(response => console.log(response))
            await axios.get('https://localhost:7189/api/Timeline?userId=' + accesstoken)
            .then(response => (tweets = response.data));

            return {
                tweets, username
            }
        
        },
        data() {
            return{
                tweetText:" ",
            };
        },
        methods:{
            sendTweet(){
                
                console.log('text: ' + this.tweetText)
            }
        }  

  }


</script>

<template>
    
    <div v-for="item in this.tweets">
        <div id="tweet">
            <div id="username">{{username}}</div>
            <div>{{item.text}}</div>
        </div>
    </div> 
    <div>
        <h1> Send Tweet</h1>
        <input type="text" v-model="tweetText" />
        <button @click="sendTweet">Send Tweet</button>

    </div>
</template>

<style>
#tweet {
    color: white;
    width: 300px;
    background-color: #A9A9A9;
    padding: 20px;
    margin: 20px;
}

#username {
    font-weight: bold;
    font-size: 20px;
    padding-bottom: 20px;
}
</style>
