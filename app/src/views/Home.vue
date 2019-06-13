<template>
<div>
  <h1> Here we'll put the Form! </h1>
    <HelloWorld msg="Hey" />
    <button @click="logout"> Logout </button>
</div>
</template>

<script>
import firebase from 'firebase';
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    HelloWorld
  },
  methods: {
    logout: function() {
      firebase.auth().signOut().then(() => {
        this.$router.replace('login')
      })
    },

  }
}
</script>
