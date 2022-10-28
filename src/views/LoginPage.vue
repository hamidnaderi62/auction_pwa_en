<template>
 <v-row  justify="center">


 <v-form >
      <v-col cols="12" justify="center" >

      <div class="text-center" >
        <v-avatar size="128" >
          <img
            :src="require('../assets/logo.png')"
            alt="Auction"
            
          >
        </v-avatar>
      </div>

        <v-text-field  
          outlined  
          v-model="username" 
          style="font-family:Vazir !important" 
          label="Username"
          :rules="[rules.required]"
        ></v-text-field>
        
        <v-text-field  
          outlined  
          v-model="password" 
          style="font-family:Vazir !important" 
          label="Password" 
          :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
          :rules="[rules.required, rules.min]"
          :type="show1 ? 'text' : 'password'"
          name="input-10-1"
          hint=""
          counter
          @click:append="show1 = !show1"
        ></v-text-field>
        
        <v-btn block  depressed color="primary" style="font-family:Vazir !important" @click="perosnLogin" >
        Login
        </v-btn>
       
      </v-col>


   </v-form>

  </v-row>


 </template>

<script>
import axios from 'axios';

  export default {
    components : {
  },
    props: [ 'auction'],
    data: () => ({
      username : '',
      password : '',   

      show1: false,
      password: '',
      rules : {
        required: value => !!value || 'required',
        min: v => v.length >= 3|| 'minimum length is 3 characters',
      },

    }),
    methods: {

        async perosnLogin(){
            await axios.post(this.$SERVER_ADDRESS + 'login', {
            username: this.username,
            password: this.password
          })
          .then(res => {
            if(res.status == '201')
            {  
              localStorage.setItem('userid' , res.data[0].code);
              localStorage.setItem('name' , res.data[0].name);
              localStorage.setItem('tel' , res.data[0].tel);
              localStorage.setItem('avatar' , res.data[0].avatar);
              this.$router.replace({  name : 'auction-page' })
                             
            }
            else{
              this.$root.SnackBar.show({message: 'Username or Password is not correct'});
            }
            
          })
          .catch( (error)  =>{
            this.$root.SnackBar.show({message: 'Username or Password is not correct'});
          });     
        },
    },

  }
</script>