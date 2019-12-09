<template>
  <div class="home">
   <QuestionAnswer v-bind:apiData="apiData[index]" v-on:next-q="nextQuestion" v-on:submit-q="submittedQ"></QuestionAnswer>
  <card v-if="maxLimitReached" class="pa-3 mx-4 ">
    <card  >
      <v-form
      ref="form"
      v-model="valid"
      :lazy-validation="lazy"
    >
      <v-container>
        <v-row>
          <v-col cols="12" sm="6" md="4">
              <v-dialog v-model="maxLimitReached "   max-width="600px" transition="dialog-bottom-transition">
                  <v-card>
                    <v-toolbar dark color="primary">
                      <v-btn icon dark @click="maxLimitReached = false">
                        <v-icon>mdi-close</v-icon>
                      </v-btn>
                      <v-toolbar-title>Mail Your Score</v-toolbar-title>
                      <v-spacer></v-spacer>
                      <v-toolbar-items>
                        <v-btn dark text :disabled="snackbar" @click="sendMail">Send
                          <v-icon>mdi-email-plus-outline</v-icon>
                        </v-btn>
                      </v-toolbar-items>
                    </v-toolbar>
                    <v-list three-line subheader>
                      <v-subheader>Your Email Here</v-subheader>
                      <v-list-item>
                        <v-list-item-content>
                          <v-list-item-subtitle class="pa-3">
                             <v-text-field   v-model="email"        :rules="emailRules"    label="E-mail"    required ></v-text-field>

                          </v-list-item-subtitle>
                        </v-list-item-content>
                      </v-list-item>
                    </v-list>
                    <v-divider></v-divider>
                  </v-card>
              </v-dialog>
          </v-col>
          <v-col>
            <v-snackbar   v-model="snackbar"  dark top :timeout="0" multi-line >
              Please provide a valid Email
                 <v-btn   color="pink"        text        @click="snackbar = false"      >     Close     </v-btn>   </v-snackbar>
          </v-col>
        </v-row>
      </v-container>
      </v-form>
    </card>
  </card>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
import QuestionAnswer from "@/components/QuestionAnswer.vue";
export default {
  name: 'home',
  components: {
    QuestionAnswer,
  },
  watch:{
    email:{
      handler(){
         if (this.$refs.form.validate()) {
          //alert(this.email);
           this.snackbar = false;
        }else{
          this.snackbar = true;
        }
      }
    }
  },
  methods:{
    nextQuestion(){
      if(this.index != 9){
        this.index++;
      }else{
        this.maxLimitReached = true;
      }
      
    },
    submittedQ(answer){
      if(this.apiData[this.index].correct_answer === answer){
         this.$emit("update",answer);
      }
      this.nextQuestion();
    },
    sendMail(){
      //alert("send");
      this.$emit("send-mail",this.email);
    },
     validate () {
       
      },
  },
  data(){
    return{
      radioGroup:1,
      apiData:[],
      index:0,
      email: '',
      snackbar:'false',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      maxLimitReached:false,
    }
  },
  created(){
    axios.get("https://opentdb.com/api.php?amount=10&type=multiple")
      .then(res =>( res.data.results.forEach(element => {
          element.incorrect_answers.push(element.correct_answer);
          this.apiData.push(element);
      })))
      .catch(); 
     
  },
  mounted(){
   
  } 
  
}
</script>
<style  scoped>
.questionholder{
  background-color : #031f1c;
}
</style>
