<template>
   <v-container class="ma-auto" >
     <v-layout row>
        <v-flex md2 xs1>
       </v-flex>
       <v-flex md8 xs10>
        <v-card class=" pa-6" color="#3f0519">
          <p class="display-1 text-center white--text"  >Compete With Quiz</p>
          <v-divider ></v-divider>
          <v-card color="#031f1c" class="questionholder">
            <p class="text-left title white--text" >
              {{apiData.question}}
            </p>
            <v-divider ></v-divider>
            <v-layout column>
              <v-flex >
                <v-card color="#031f1c" class="">
                  <v-radio-group v-model="radioGroup" class="pa-0" >
                    <v-chip color="#3f0519" v-for="n in apiData.incorrect_answers"  :key="n" class="ma-3">
                        <v-radio  class="pa-5 headline" dark   :label="` ${n}`"    :value="n"   >
                        </v-radio>
                    </v-chip>
                  </v-radio-group>
                </v-card>
              </v-flex>
              <v-flex md2>
                <p class="text-center">
                  <v-btn   outlined class="white--text" v-on:click="nextClicked"> Next</v-btn>
                  <v-btn  class="green white--text" :disabled="radioGroup === null" v-on:click="answerSubmitted">Submit</v-btn>
                </p>
              
              </v-flex>
            </v-layout>
          </v-card>

      </v-card>

       </v-flex>
        <v-flex md2 xs1>
       </v-flex>
     </v-layout>
    
    </v-container>
</template>

<script>
import _ from 'lodash';
export default {
  name:"questionAnswer",
  props:["apiData"],
  methods:{
    answerSubmitted(){
      this.$emit('submit-q',this.radioGroup);
      this.radioGroup =null;

    },
    nextClicked(){
      this.$emit('next-q');
       this.radioGroup =null;

    }
  },
  data() {
    return{
      
      radioGroup:null,
    }
  },
  watch:{
    apiData:{
      
      handler(){
        //this.apiData.correct_answer='';
        this.apiData.incorrect_answers = _.shuffle(this.apiData.incorrect_answers);
      }
    }
  }
  
}
</script>

<style>

</style>