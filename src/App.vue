<template>
  <v-app>
   <CreatePassword />

  </v-app>
</template>

<script>
import CreatePassword from './components/CreatePassword.vue';

export default {
    name: "App",
    data: () => ({
    //
    }),
    components: { CreatePassword }
};
</script>
