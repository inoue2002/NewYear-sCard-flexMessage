<template>
  <div>
    <!-- <v-btn @click="click"> hello </v-btn> -->
    <v-row justify="center" style="margin-top: 10px">
      <v-col cols="11" md="8">
        <p>
          <v-text
            >このサービスを使うと簡単にLINE友達に自分で作成した年賀状を一斉送信することができるサービスです。✨</v-text
          >
        </p>
        <p><v-text>▼以下のような年賀状を作成&送信できます</v-text></p>
        <v-img
          width="70%"
          src="https://pbs.twimg.com/media/EqkFdACU0AEE0Qu?format=jpg&name=medium"
        />
        <form class="button_form_center" style="margin-top: 30px">
          <v-btn Block color="#0096db" href='new'>
            <span style="color: white" 
              >今すぐオリジナル年賀状を作る!!</span
            ></v-btn
          >
        </form>
      </v-col>
    </v-row>
  </div>
</template>

<script>

export default {
  components: {
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
      .then((data) => {
        console.log(`init完了`);
      });

    // ログインチェック
    if (liff.isLoggedIn()) {
    } else {
      // ログインまだ
      //liff.login();
    }
  },
  methods: {
  },
};
</script>

<style scaped>
.button_form_center {
  text-align: center;
}
</style>
