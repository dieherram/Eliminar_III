<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn v-if="currentUser" text>
        <span class="mr-2" @click.prevent="logout">Cerrar Sesión</span>
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import firebase from 'firebase'
import { mapState, mapActions } from 'vuex'
export default {
  name: 'App',

  data: () => ({
  }),
  computed: {
...mapState(["currentUser"])
  },
  methods:{
    ...mapActions(["setCurrentUser"]),
    logout(){
      firebase.auth().signOut().then(()=>{
        this.setCurrentUser(null)
        this.$router.push('/login')
      })
    }
  },
  created(){
this.setCurrentUser(firebase.auth().currentUser)
  }
};
</script>
