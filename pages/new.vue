<template>
  <div>
    <!-- <v-btn @click="click"> hello </v-btn> -->
    <v-row justify="center" style="margin-top: 10px">
      <v-col cols="11" md="8">
        <p><v-text>▼以下のような年賀状を作成&送信できます</v-text></p>
        <v-img
          width="70%"
          src="https://pbs.twimg.com/media/EqkFdACU0AEE0Qu?format=jpg&name=medium"
        />
        <form class="button_form_center" style="margin-top: 30px">
          <v-btn @click="click" Block color="#0075c2">
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
  methods: {
    click() {
      console.log(`trueOrFolse`, liff.isApiAvailable("shareTargetPicker"));
      if (liff.isApiAvailable("shareTargetPicker")) {
        liff
          .shareTargetPicker([
            ///ターゲットぴっかーで送るメッセージはここから
            {
              type: "flex",
              altText: "年賀状が届きました!!",
              contents: {
                type: "bubble",
                direction: "ltr",
                header: {
                  type: "box",
                  layout: "vertical",
                  position: "relative",
                  contents: [
                    {
                      type: "text",
                      text: "はっぴーにゅーいやー!!",
                      weight: "bold",
                      size: "md",
                      color: "#3C2626FF",
                      align: "center",
                      wrap: true,
                      contents: [],
                    },
                  ],
                },
                hero: {
                  type: "image",
                  url:
                    "https://online.brother.co.jp/BOL/Handlers/DownloadContents400x400.ashx?id=6db6456c-99b9-4a7c-8011-aac4ef92544f",
                  margin: "none",
                  size: "3xl",
                  aspectRatio: "1.51:1",
                  aspectMode: "fit",
                  position: "relative",
                },
                body: {
                  type: "box",
                  layout: "vertical",
                  spacing: "none",
                  margin: "none",
                  contents: [
                    {
                      type: "text",
                      text: "今年もよろしくお願いします！",
                      weight: "bold",
                      size: "sm",
                      align: "center",
                      margin: "none",
                      wrap: true,
                      contents: [],
                    },
                    {
                      type: "text",
                      text: "ようかんより",
                      weight: "bold",
                      size: "xs",
                      align: "end",
                      margin: "sm",
                      wrap: true,
                      contents: [],
                    },
                  ],
                },
                footer: {
                  type: "box",
                  layout: "horizontal",
                  contents: [
                    {
                      type: "button",
                      action: {
                        type: "uri",
                        label: " by New Year's Card",
                        uri: "https://liff.line.me/1655537683-Qgj6p10A",
                      },
                    },
                  ],
                },
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
.button_form_center {
  text-align: center;
}
</style>
