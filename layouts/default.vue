<template>
  <v-app dark>

      <v-app-bar
        color="deep-purple accent-4"
        dense
        dark

      >
        <v-app-bar-nav-icon></v-app-bar-nav-icon>
  
        <v-toolbar-title>Page title</v-toolbar-title>
  
        <v-spacer></v-spacer>
  

        <v-menu
          left
          bottom
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              @click="toggleActivity"
            >
              Upload
            </v-btn>
          </template>
        </v-menu>
      </v-app-bar>
      <videoUpload/>
   <v-main>
        <nuxt />
    </v-main>
   
 
  </v-app>
</template>

<script>

  import {mapMutations} from 'vuex'
  import videoUpload from "../components/videoUpload"

export default {
  components: { videoUpload },
      methods: mapMutations ('videoUpload',['toggleActivity'])
}
</script>
