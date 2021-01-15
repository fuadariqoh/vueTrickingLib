<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <div class="text-center">
        <logo />
        <vuetify-logo />
      </div>
      <v-card>
        <v-card-title class="headline">
           {{message}} 
           <v-btn @click="reset">Reset </v-btn>
           <v-btn @click="resetTricks">Reset Trick </v-btn>

        </v-card-title>
        <div v-if="tricks">
            <p v-for="t in tricks"> 
              {{t.name}}
            </p>
        </div>

        <div>
          <v-input label="" v-model="trickName" />
           <v-btn @click="saveTrick">Save Trick </v-btn>

        </div>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            nuxt
            to="/inspire"
          >
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script lang="ts">
import Logo from "../components/Logo.vue"
import VuetifyLogo from "../components/VuetifyLogo.vue"
import Axios from "axios"
import {mapState, mapActions, mapMutations} from "vuex"

export default {
  components: {
    Logo,
    VuetifyLogo
  },
  data:()=>({
    trickName:""
  }),
  
  computed :{
    ...mapState({
    message:state => state.message
  }),
   ...mapState('tricks',{
    tricks:state => state.tricks
  })},
  methods : {
    
    ...mapMutations([
    'reset'
  ]),
    ...mapMutations({
      resetTricks:'reset'
    }),
  ...mapActions('tricks',["createTricks"]),
  async saveTrick(){
    // await this.createTricks({trick:{name:this.trickName}})
    console.log("testing")
  }
  
  },
  // async fetch(){
  //   await this.$store.dispatch(`fetchMessage`)
  // }
  // asyncData(payload:String){
  //    return Axios.get("http://localhost:5000/api/home")
  //     .then(({data})=>{
  //           return { message :data}
  //     })
  // },
 
}
</script>
