<template>
  <v-app>
     <v-container  fluid>

       <v-layout mt-12 align-center justify-space-around  wrap>

          <v-flex   xs12 md4 ma-1>
           <div class="text-f">
            <v-text-field
            rounded
            v-model="eng_word"
            label="Solo"
            placeholder="Enter English Text"
            solo
          ></v-text-field>
           </div>
            
            <v-radio-group v-model="language" row>
      <v-radio label="Russian" value="ru"></v-radio>
      <v-radio label="French" value="fr"></v-radio>
      <v-radio label="Latin" value="la"></v-radio>
        <v-radio label="Chinese" value="zh"></v-radio>
    </v-radio-group>
          
          <div class="text-center">
          <v-btn rounded
           color="success"
           @click="translate"
           >Translate</v-btn>
          </div>

      </v-flex>
    
      <v-flex xs12 md4 ma-1>
        <v-card dark class="text-d" height="200px" flat>
           <div class="text-center">
          <v-card-text >Translation</v-card-text>
          <v-card-text class="display-2" >{{translation}}</v-card-text>
           </div>
        </v-card>
      </v-flex>

       </v-layout>
     </v-container>
  </v-app>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  components: {

  },
  data: () => ({
    language: "ru",
    eng_word: "",
    translation:""
  }),
  methods:{
    translate(){
      try {
         axios.get(`https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20190804T065058Z.dc1f9e38631388bb.104ca214624880a09302466c7c9a7da5116c79d6&lang=${this.language}&text=${this.eng_word}`)
       .then(res=>{
         console.log(res.data.text[0])
         this.translation=res.data.text[0]
       })
      } catch (error) {
        console.log(error)
      }
      
      
    }
  },
};
</script>

<style scoped>
.text-f{
  margin-top: 150px
}
.text-d{
  margin-top: 100px
}
</style>
