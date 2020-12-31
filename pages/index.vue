<template>
  <div>
    <v-btn @click="click"> hello </v-btn>
    {{id}}
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
      id: 0,
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
      this.id = this.id +1
      if (liff.isApiAvailable("shareTargetPicker")) {
        console.log(liff.isApiAvailable("shareTargetPicker"))
        liff.shareTargetPicker([
          {
            type: "text",
            text: "Hello, World!",
          },
        ]);
      }
    },
  },
};
</script>

<style scaped>
</style>
