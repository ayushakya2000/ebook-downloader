<template>
  <v-parallax src="https://firebasestorage.googleapis.com/v0/b/new111-87012.appspot.com/o/camera-coffee-colorful-1391374.jpg?alt=media&token=e3a92fe8-3755-461b-b500-598f76f56317" height="100%">
  <v-app style = "background: rgb(0,0,0,0)">
    <v-toolbar app color="rgb(0,0,0,0.5)">
      <v-toolbar-title class="headline text-uppercase" dark>
        <span class=" grey--text">get</span>
        <span class="font-weight-light white--text">placed</span>
      </v-toolbar-title>
    </v-toolbar>
    <v-layout align-center justify-center>
    <v-flex xs12 sm6 md5 lg4>
      <v-card color="rgb(0,0,0,0.5)">
        <!--<v-img
          class="white--text"
          lazy-src
          gradient="to top right, rgba(100,115,201,.33), rgba(25,32,72,.1)"
          height="175px"
          src="https://firebasestorage.googleapis.com/v0/b/new111-87012.appspot.com/o/Glitter-Bokeh-Wallpaper-HD-24857.jpg?alt=media&token=917fc0fd-82e7-4ae2-a930-e4ad04fa8def"
        >
        </v-img>-->
        <br>
        <v-card-title>
          <v-layout row wrap align-center justify-center>
            <span class = "grey--text display-1 display-1 lighten-4">GET</span>
            <span class = "white--text display-1 font-weight-light">Connected</span>
          </v-layout>
        </v-card-title>
        
        <v-layout justify-center>
          <v-card-actions>
            <v-btn @click="signupGoogle" color="#3b5998" dark large><v-icon small left>fab fa-facebook</v-icon>Facebook</v-btn>
            
            <v-btn @click="signupFacebook" color="#db4a39" dark large><v-icon small left>fab fa-google</v-icon>Google</v-btn>
          </v-card-actions>
        </v-layout>
        <br>
      </v-card>
    </v-flex>
  </v-layout>
  </v-app>
  </v-parallax>
</template>

<script>
  import firebase from 'firebase';
  import axios from 'axios';

  export default {
    name: 'login',

    methods: {
      
      signupGoogle: function() {
        var provider = new firebase.auth.GoogleAuthProvider();
        firebase.auth().signInWithRedirect(provider);
        firebase.auth().getRedirectResult().then(function(result) {
        if (result.credential) {
          // This gives you a Google Access Token. You can use it to access the Google API.
          var token = result.credential.accessToken
          // ...
        }
        // The signed-in user info.
        var user = result.user
        this.$router.replace('home')
        }).catch(function(error) {
          // Handle Errors here.
          var errorCode = error.code
          var errorMessage = error.message
          // The email of the user's account used.
          var email = error.email
          // The firebase.auth.AuthCredential type that was used.
          var credential = error.credential
          // ...
        });
    },

    signupFacebook: function() {
      var provider = new firebase.auth.FacebookAuthProvider();
      firebase.auth().signInWithRedirect(provider);
      firebase.auth().getRedirectResult().then(function(result) {
      if (result.credential) {
        // This gives you a Facebook Access Token. You can use it to access the Facebook API.
        var token = result.credential.accessToken;
        // ...
      }
      // The signed-in user info.
      var user = result.user;
      this.$router.replace('home')
    }).catch(function(error) {
      // Handle Errors here.
      var errorCode = error.code;
      var errorMessage = error.message;
      // The email of the user's account used.
      var email = error.email;
      // The firebase.auth.AuthCredential type that was used.
      var credential = error.credential;
      // ...
    });
    }
  }
}
</script>