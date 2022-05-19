<template>
  <v-app>
    <div class="container">
        <v-main>
          <router-view/>
      </v-main>
    </div>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
