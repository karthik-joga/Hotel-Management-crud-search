<template>
<div class="mx-10">
     <v-app-bar class="orange" dense app flat height="70">
       <p class="white--text text-h5 ml-10 mt-5" id="logo">Hotel Booking</p>
      
   </v-app-bar>
   <div v-text="header" class="text-h4 orange--text"></div>
    <form  class="mx-10 my-5"  @submit.prevent="create">
      <div id="form"
      class="d-flex flex-wrap ma-10 ">      
       <v-col
          cols="12"
          sm="6"
          md="3"
        >
          <v-text-field
            label="Full Name"
            outlined
            color="orange"
            dense
            flat
            v-model="formData.name"
          ></v-text-field>
        </v-col>
         <v-col
          cols="12"
          sm="6"
          md="3"
        >
          <v-text-field
            label="Age"
            outlined
            type="number"
            color="orange"
            dense
            flat
            v-model="formData.age"
          ></v-text-field>
        </v-col>
         <v-col
          cols="4"
          sm="6"
          md="3"
        >
          <v-text-field
            label="Phone Number"
            outlined
            type="number"
            color="orange"
            dense
            flat
            v-model="formData.phoneno"
          ></v-text-field>
        </v-col>
        <v-col
          cols="4"
          sm="6"
          md="3"
        >
          <v-text-field
            label="Email"
            outlined
            type="email"
            color="orange"
            dense
            flat
            v-model="formData.email"
          ></v-text-field>
        </v-col>
    

     <div class="d-block">
        <v-radio-group
      v-model="formData.gender"
      row
    >
   
     <p class="ml-5 mt-4">Gender</p> <v-radio
      class="ml-5"
        label="Male"
        value="male"
        color="orange"
        
      ></v-radio>
      <v-radio
        label="Female"
        value="Female"
        color="orange"
        
      ></v-radio>
      
    </v-radio-group>
    </div>
    <v-col
          cols="12"
          sm="6"
          md="3"
        >
          <v-text-field
            label="number of persons"
            outlined
            type="number"
            color="orange"
            dense
            flat
            v-model.number="formData.noper"
          ></v-text-field>
        </v-col>

           <v-radio-group
      v-model="formData.noofroom"
      row
    >
      Number of Rooms  <v-radio
        label="1"
        class="ml-5"
        value="1"
        color="orange"
        
      ></v-radio>
      <v-radio
        label="2"
        value="2"
        color="orange"
        
      ></v-radio>
       <v-radio
        label="3"
        value="3"
        color="orange"
        
      ></v-radio>
    </v-radio-group>
      <v-col
          cols="12"
          sm="6"
          md="3"
        >
          <v-text-field
            label="fromDate"
            outlined
            type="date"
            color="orange"
            dense
            flat
            v-model="formData.fromDate"
          ></v-text-field>
        </v-col>

         <v-col
          cols="12"
          sm="6"
          md="3"
        >
          <v-text-field
            label="ToDate"
            outlined
            type="date"
            color="orange"
            dense
            flat
            v-model="formData.toDate"
          ></v-text-field>
        </v-col>

       <v-col
          cols="12"
          sm="6"
          md="3"
        >
        <v-select
        :items="item"
        label="Select location"
        v-model="formData.loc"
        >

        </v-select>
        </v-col>

     <v-col
        cols="12"
        sm="4"
      >
        <v-textarea
        v-model="formData.purpose"
          filled
          auto-grow
          label="Purpose"
          rows="2"
          row-height="40"
          color="orange"
        ></v-textarea></v-col>
        </div>
      <v-btn class="ml-10" v-show="sub" @click="create" color="orange" outlined>Submit</v-btn>
      <v-btn class="ml-10" v-show="up" @click="update" color="orange" outlined>Update</v-btn>
    </form>
</div>
</template>
   


<script>
import Axios from "axios"
import Vue from 'vue'
    export default {
        data() {
            return {
            formData: {
                name:"",
                age:"",
                gender:"",
                email:"",
                phoneno:"",
                noper:"",
                purpose:"",
                noofroom:0,
                fromDate:"",
                toDate:"",
                loc:""
            },
            number:"",
            sub:true,
            up:false,
            header:"Booking",
            item:["Banglore","vizag","Hyderbad","Tamilnadu"]
            }
        },
        methods: {
            create(){
               if(this.formData.age > 0 ){
                 Axios.post("http://localhost:4000/hotel",this.formData)
                 this.formData.name="",
                 this.formData.age="",
                 this.formData.email="",
                 this.formData.phoneno="",
                this.formData.noper="",
                this.formData.purpose="",
                 this.formData.noofroom=""
                 this.formData.gender=""
                 this.$router.push("/")
               }else{
                 Vue.$vToastify.error("enter the age")
               }
            },
          async get(num){
              this.number=num
              this.sub=false
              this.up=true
               let b= await Axios.get(`http://localhost:4000/hotel/${num}`)
               this.formData.name=b.data.name,
                 this.formData.age=b.data.age,
                 this.formData.email=b.data.email,
                 this.formData.phoneno=b.data.phoneno,
                this.formData.noper=b.data.noper,
                this.formData.purpose=b.data.purpose,
                 this.formData.noofroom=b.data.noofroom
                 this.formData.gender=b.data.gender
                 this.formData.fromDate=b.data.fromDate
                  this.formData.toDate=b.data.toDate
                   this.formData.loc=b.data.loc
            this.header="Edit Details"
           },
           update(){
            
                Axios.put(`http://localhost:4000/hotel/${this.number}`,this.formData)
                this.$router.push("/")
                console.log(this.formData)
                
           }
        },
        created() {
           let key=this.$route.params
            if(key.id > 0){
                this.get(key.id)
            }
        }
       
    }
</script>

<style scoped>
#form {
    flex-wrap:wrap;
   
}
#logo::first-letter {
   font-size: 40px;
}
</style>