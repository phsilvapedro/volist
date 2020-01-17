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
          :src="require('./assets/volanty.png')"
          transition="scale-transition"
          width="150"
        />

      </div>

      <v-spacer></v-spacer>
      
    </v-app-bar>

    <v-content>
      <Cars/>
    </v-content>
  </v-app>
</template>

<script>
import Cars from './components/Cars';

export default {
  name: 'App',

  components: {
    Cars,
  },

  data: () => ({
    //
  }),
};
</script>