<template>
  <v-app dark>
    <v-app-bar fixed app color="#00db45">
      <nuxt-link to="/" class="title head-text pa-0 cursor: pointer;">
        <v-img
          max-width="125px"
          src="https://pbs.twimg.com/media/EqkaANTUcAEe0RO?format=jpg&name=small"
        />
      </nuxt-link>
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>&copy; 2020/2021 ようかん</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-apps",
          title: "Welcome",
          to: "/",
        },
        {
          icon: "mdi-chart-bubble",
          title: "Inspire",
          to: "/inspire",
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "LINEで年賀状",
    };
  },
};
</script>

