<template>
      <v-dialog
       :value="active"
        width="800"
        persistent
      >
    <v-stepper v-model="step">
      <v-stepper-header>
        <v-stepper-step
          :complete="step > 1"
          step="1"
        >
          Select Type 
        </v-stepper-step>
  
        <v-divider></v-divider>
  
        <v-stepper-step
          :complete="step > 2"
          step="2"
        >
          Upload Video 
        </v-stepper-step>
  
        <v-divider></v-divider>
  
        <v-stepper-step step="3">
            Trick Information
        </v-stepper-step>
        <v-stepper-step step="4">
            Review
        </v-stepper-step>
      </v-stepper-header>
  
      <v-stepper-items>
           <v-stepper-content step="1">
          <div class="d-flex flex-column align-center">
            <v-btn class="my-2" @click="setType(uploadType.TRICK)" >Trick</v-btn>
            <v-btn class="my-2" @click="setType(uploadType.SUBMISSION)" >Submission</v-btn>
          </div>
  
        </v-stepper-content>
        <v-stepper-content step="2">
          <div>
            <v-file-input
              accept="video/*"
              @change="handleFile"

            truncate-length="10"
          ></v-file-input>
          </div>
  
        </v-stepper-content>
  
        <v-stepper-content step="3">
          <div>
          <!-- <v-input label="" v-model="trickName" /> -->
          <v-text-field label="tricking name" v-model="trickName"></v-text-field>
           <v-btn @click="saveTrick">Save Trick </v-btn>

        </div>


        </v-stepper-content>
  
        <v-stepper-content step="4">
          <div>
              Success
            </div>
        </v-stepper-content>
      </v-stepper-items>
    </v-stepper>
  
  <div class="d-flex justify-center my-5">
          <v-btn @click="toggleActivity">
            Close
          </v-btn>
        </div>
      </v-dialog>
</template>

<script>
import {mapState, mapActions, mapMutations} from "vuex"
import {UPLOAD_TYPE} from "../data/enum"

export default{

data:()=>({
    trickName:"",
  }),

  computed:{
        ...mapState('videoUpload',['uploadPromise','active','step']),
      uploadType(){
        return{
          ...UPLOAD_TYPE
        }
      },
  },
   methods : {
    ...mapMutations('videoUpload',['reset','toggleActivity','setType']),
  ...mapActions('videoUpload',['startVideoUpload','createTricks']),

  async handleFile(file){
      if(!file) return;

        const form= new FormData()
        form.append("video",file)
        this.startVideoUpload({form})
        this.step++;
  },

    async saveTrick(){
    if(!this.uploadPromise){
      console.log("upload task null")
      return ;
    }
    const video= await this.uploadPromise
    await this.createTricks({trick:{name:this.trickName,video}}) 
    this.trickName=""
    this.reset()
  },
},
}
</script>

