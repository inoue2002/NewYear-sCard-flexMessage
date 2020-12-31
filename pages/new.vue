<template>
  <div>
    <v-row justify="center" style="margin-top: 10px">
      <v-col cols="11" md="8">

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
     // liff.login();
    }
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
