<template>
  <div>
    <v-btn @click="click"> hello </v-btn>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";
import VuetifyLogo from "~/components/VuetifyLogo.vue";

export default {
  components: {
    Logo,
    VuetifyLogo,
  },
  data() {
    return {
      id: "",
      userInfo: "",
      userName: "",
      res: "",
    };
  },
  async mounted() {
    await liff
      .init({
        liffId: "1655537683-Qgj6p10A",
      })
      .catch((err) => {
        this.res = "initErr";
      })
      .then((data) => {});

    // ログインチェック
    if (liff.isLoggedIn()) {
    } else {
      // ログインまだ
      liff.login();
    }
  },
  methods: {
    click() {
      liff.shareTargetPicker([
        {
          type: "text",
          text: "Hello, World!",
        },
      ]);
    },
  },
};
</script>

<style scaped>
</style>
