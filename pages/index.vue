<template>
<div>
<div v-if="tricks">
<div v-for="t in tricks">
    {{t.name}}
    {{t.video}}
    <div>
        <video width="400" height="400" :src="`http://localhost:5000/api/videos/${t.video}`">
        </video>
    </div>
</div>

</div>


  

</div>

</template>

<script lang="ts">
import {mapState, mapActions, mapMutations} from "vuex"
import {UPLOAD_TYPE} from "../data/enum"

export default {
  data:()=>({
    trickName:"",
  }),
  
  computed :{
   ...mapState('tricks',['tricks']),
  },
}
</script>
