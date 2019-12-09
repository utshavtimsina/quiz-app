<template>
  <v-app>
    <Navbar v-bind:correct="correct"></Navbar>
    <v-content>
      <router-view v-on:update="updateSuccesfullAnswers" v-on:send-mail="sendmailto"></router-view>
    </v-content>
  </v-app>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
export default {
  name: 'App',

  components: {
    Navbar,
  },
  methods:{
    updateSuccesfullAnswers(ans){
     // alert(ans);
    
      this.ans = ans;
      this.correct++;
    },
    sendmailto(email){
      console.log(email);
    }
  },
  data: () => ({
    //
    correct:'0',
    ans:''

  }),
};
</script>
