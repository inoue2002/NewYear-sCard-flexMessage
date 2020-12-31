<template>
  <div>
    <v-btn @click="click"> hello </v-btn>
    {{ id }}
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
      .then((data) => {
        console.log(`init完了`);
      });

    // ログインチェック
    if (liff.isLoggedIn()) {
    } else {
      // ログインまだ
      liff.login();
    }
  },
  methods: {
    click() {
      this.id = this.id + 1;
      console.log(`trueOrFolse`, liff.isApiAvailable("shareTargetPicker"));
      if (liff.isApiAvailable("shareTargetPicker")) {
        liff
          .shareTargetPicker([
            ///ターゲットぴっかーで送るメッセージはここから
            {
              type: "flex",
              altText: "flexMessageです",
              contents: {
  "type": "bubble",
  "direction": "ltr",
  "header": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "Header",
        "align": "center",
        "contents": []
      }
    ]
  },
  "hero": {
    "type": "image",
    "url": "https://vos.line-scdn.net/bot-designer-template-images/bot-designer-icon.png",
    "size": "full",
    "aspectRatio": "1.51:1",
    "aspectMode": "fit"
  },
  "body": {
    "type": "box",
    "layout": "vertical",
    "contents": [
      {
        "type": "text",
        "text": "Body",
        "align": "center",
        "contents": []
      }
    ]
  },
  "footer": {
    "type": "box",
    "layout": "horizontal",
    "contents": [
      {
        "type": "button",
        "action": {
          "type": "uri",
          "label": "Button",
          "uri": "https://linecorp.com"
        }
      }
    ]
  }
},
            },
            /////ターゲットぴっかーで送るのはここまで
          ])
          .then(function (res) {
            if (res) {
              // succeeded in sending a message through TargetPicker
              console.log(`[${res.status}] Message sent!`);
            } else {
              const [majorVer, minorVer] = (liff.getLineVersion() || "").split(
                "."
              );
              if (parseInt(majorVer) == 10 && parseInt(minorVer) < 11) {
                // LINE 10.3.0 - 10.10.0
                // Old LINE will access here regardless of user's action
                console.log(
                  "TargetPicker was opened at least. Whether succeeded to send message is unclear"
                );
              } else {
                // LINE 10.11.0 -
                // sending message canceled
                console.log("TargetPicker was closed!");
              }
            }
          })
          .catch(function (error) {
            // something went wrong before sending a message
            console.log("something wrong happen");
          });
      }
    },
  },
};
</script>

<style scaped>
</style>
