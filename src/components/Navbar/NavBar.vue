<template>
<div>
   <v-app-bar class="orange" dense app flat height="70">
       <p class="white--text text-h4 ml-10 mt-5" id="logo">Hotel</p>
       <v-spacer></v-spacer>
       
        
       
       <router-link to="/book" style="text-decoration:none">
           <v-btn class="white--text" elevation="0" outlined>BookNow</v-btn>
       </router-link>
   </v-app-bar>
  
   </div>
</template>

<script>
import Axios from 'axios'
    export default {
        data(){
            return {
            
            }
        },
        methods: {
           async hotel() {
               let take=await Axios.get("http://localhost:4000/places")
               this.items=take.data
            console.log(take.data)
            }
        },
        
    }
</script>

<style scoped>
#logo::first-letter {
   font-size: 40px;
}
</style>