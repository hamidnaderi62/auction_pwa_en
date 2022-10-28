<template>
  <v-card
    max-width="400"
    class="mx-auto"
  >


    <v-card-text>

    <v-col cols="12" align="center" justify="space-around" >
    <v-text-field outlined :rules="[rules.required]"  v-model="title" style="font-family:Vazir !important" label="Title"></v-text-field>
    <v-text-field outlined :rules="[rules.required]" v-model="basePrice" style="font-family:Vazir !important" label="Base Price"></v-text-field>
    <v-text-field outlined :rules="[rules.required, rules. deadline]" v-model="availableDays" style="font-family:Vazir !important" label="Deadline"></v-text-field>
    <v-textarea outlined  v-model="features" style="font-family:Vazir !important" label="Features"></v-textarea>
    <v-textarea outlined  v-model="desc" style="font-family:Vazir !important" label="Description"></v-textarea>
    <v-text-field outlined :rules="[rules.required]" v-model="image1" style="font-family:Vazir !important" label="Image1"></v-text-field>
    <v-text-field outlined  v-model="image2" style="font-family:Vazir !important" label="Image2"></v-text-field>
    <v-text-field outlined  v-model="image3" style="font-family:Vazir !important" label="Image3"></v-text-field>
      <v-btn block  depressed color="primary" style="font-family:Vazir !important" @click="createAuction" >
        Send
      </v-btn>
    </v-col>
    
  

    </v-card-text>
  </v-card>
</template>

<script>

import axios from 'axios';


  export default {
    components : {
  },
    props: [ 'auction'],
    data: () => ({
      title : '',
      basePrice : '',
      availableDays : '',
      desc : '',
      features : '',
      image1 : '',
      image2 : '',
      image3 : '',   
      rules : {
        required: value => !!value || 'required',
        min: v => v.length >= 3|| 'minimum length is 3 characters',
        deadline: value => value > 0|| 'must be bigger than 0',
      },
       
    }),

    methods: {

        createAuction(){
          if(localStorage.getItem('userid')){
            axios.post(this.$SERVER_ADDRESS + 'auction', {
            title : this.title,
            desc : this.desc,
            features : this.features,
            basePrice : this.basePrice, 
            image1 : this.image1,
            image2 : this.image2,
            image3 : this.image3,
            availableDays : this.availableDays,
            personID : localStorage.getItem('userid')
          })
          .then((response) =>{
            this.$root.SnackBar.show({message: 'Your auction registered successfully'});
          })
          .catch((error) => {
            console.log(error);
          });     

          }      
        },
    },

  }
</script>