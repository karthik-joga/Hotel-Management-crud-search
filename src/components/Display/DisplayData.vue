<template>
    <div>
        <v-col cols="12" sm="4">
        <v-text-field width="10" label="search with name" color="orange" @keyup="data_Filter" v-model="filt"></v-text-field>  
        </v-col>
    <v-simple-table>
         
        <thead>
            <tr >
                <th class="text-body-1 text-bold orange--text">Name</th>
                <th class="text-body-1 text-bold orange--text">Age</th>
                <th class="text-body-1 text-bold orange--text">Email</th>
                <th class="text-body-1 text-bold orange--text">Phone number</th>
                <th class="text-body-1 text-bold orange--text">Gender</th>
                <th class="text-body-1 text-bold orange--text">Persons</th>
                <th class="text-body-1 text-bold orange--text">Rooms</th>
                <th class="text-body-1 text-bold orange--text">From</th>
                <th class="text-body-1 text-bold orange--text">To</th>
                <th class="text-body-1 text-bold orange--text">Location</th>
                <th class="text-body-1 text-bold orange--text">Purpose</th>
                <th class="text-body-1 text-bold orange--text">Delete</th>
            </tr>
        </thead>
        <tbody>
            
                <tr  v-for="detail in details" :key="detail.id">
                <td @click="edit(detail.id)">{{detail.name}}</td>
                <td @click="edit(detail.id)">{{detail.age}}</td>
                <td @click="edit(detail.id)">{{detail.email}}</td>
                <td @click="edit(detail.id)">{{detail.phoneno}}</td>
                <td @click="edit(detail.id)">{{detail.gender}}</td>
                <td @click="edit(detail.id)">{{detail.noper}}</td>
                <td @click="edit(detail.id)">{{detail.noofroom}}</td>
                <td @click="edit(detail.id)">{{detail.fromDate}}</td>
                <td @click="edit(detail.id)">{{detail.toDate}}</td>
                <td @click="edit(detail.id)">{{detail.loc}}</td>
                <td @click="edit(detail.id)">{{detail.purpose}}</td>
                <td><v-btn @click="remove(detail.id)" outlined fab small color="orange" class="btn"><v-icon>mdi-delete</v-icon></v-btn></td>
                </tr>
            
        </tbody>
    </v-simple-table>
    </div>
</template>

<script>
    import Axios from 'axios'
    export default {
        data() {
            return{
                details:[],
                filt:""
            }
        },
        methods: {
            async take(){
                let b=await Axios.get("http://localhost:4000/hotel")
                this.details=b.data
                console.log(this.details)
            },
            edit(num){
                this.$router.push(`/edit/${num}`)
            },
            data_Filter(){
                if(this.filt.length > 0){
                this.details.map(x=>{
                    if(this.filt === x.name){
                        this.details=[x]
                    }
                })}else{
                    this.take()
                }
                
                // for(let i=0;i<=this.details.length;i++){
                //     if(this.filt=== this.details[i].name){
                //         this.details=[this.details[i]]
                //     }
                // }
            },
            remove(id){
                Axios.delete(`http://localhost:4000/hotel/${id}`)
                // this.$router.push('/')
                this.take()
            }
        },
        beforeMount() {
            let val=typeof this.$route.params
            if( val === 'object'){
                  setTimeout( this.take(),5000)
            }
        }
    }
</script>

<style scoped>
.btn:hover {
    background-color: rgb(243, 73, 73);
    
}
</style>