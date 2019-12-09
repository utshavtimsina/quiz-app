<template>
  <v-app-bar
      app
      dark
    >
    <v-app-bar-nav-icon></v-app-bar-nav-icon>
    <v-toolbar-title>Quiz App</v-toolbar-title>
    <v-spacer></v-spacer>
    <v-toolbar-title class="title">
      Correct 
    </v-toolbar-title>
    <v-toolbar-title class="mx-2">
      <span class="headline mx-2" >{{correct}} <v-divider></v-divider>10</span>
    </v-toolbar-title>
    <v-icon>
      mdi-bookmark-check
    </v-icon>
    <v-spacer></v-spacer>
    </v-app-bar>
</template>

<script>
export default {
    name:"Navbar",
    props:['correct'],
    data(){
        return{
             corrects:this.correct,
        }
    },
    //
   
    

  
}
</script>

<style>

</style>