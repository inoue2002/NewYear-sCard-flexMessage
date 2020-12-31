<template>
  <div>
    <v-row justify="center" style="margin-top: 10px">
      <v-col cols="11" md="8">
        <v-stepper v-model="e1">
          <v-stepper-header>
            <template v-for="n in steps">
              <v-stepper-step
                :key="`${n}-step`"
                :complete="e1 > n"
                :step="n"
                editable
              >
                Step {{ n }}
              </v-stepper-step>

              <v-divider v-if="n !== steps" :key="n"></v-divider>
            </template>
          </v-stepper-header>

          <v-stepper-items>
            <v-stepper-content
              v-for="n in steps"
              :key="`${n}-content`"
              :step="n"
            >
              <!-- タイトルを決めてもらう -->
              <v-card class="mb-12" color="" height="200px" v-if="n === 1" flat　style='margin-bottom:100px'>
                <v-row justify="center" align-content="center">
                  <v-col cols="12">
                    <p><v-text>タイトルを入力してください</v-text></p>
                    <v-textarea
                    v-model="titile"
                      auto-grow
                      outlined
                      rows="1"
                      row-height="15"
                    ></v-textarea>
                    <v-img
                      width="20%"
                      src="https://pbs.twimg.com/media/EqkS1AOVgAAbEZT?format=png&name=240x240"
                    />
                  </v-col>
                </v-row>
              </v-card>
              <!-- 画像を決めてもらう -->
              <v-card class="mb-12" color="" height="200px" v-if="n === 2" flat>
                <v-row justify="center">
                  <v-col cols="12">
                    <p><v-text>現在は選択できません。そのまま次へ進んでください。jpgの画像URLをお持ちの方は下記に入力してください。</v-text></p>
                   <v-textarea
                    v-model="url"
                      auto-grow
                      outlined
                      rows="1"
                      row-height="15"
                    ></v-textarea>
                    <p><v-text>▼プレビュー</v-text></p>
                    <v-img width=10% :src='url' />
                    </v-col>
                </v-row>
              </v-card>

              <!-- コンテンツを決めてもらう　メッセージと誰からか -->
              <v-card class="mb-12" color="" height="200px" v-if="n === 3" flat>
                <v-row justify="center">
                  <v-col cols="12">
                    <v-textarea
                     v-model="message"
                      name="input-7-4"
                      label="Message"
                    ></v-textarea>
                    <v-textarea
                     v-model="from"
                      label="YourName"
                      auto-grow
                      outlined
                      rows="1"
                      row-height="15"
                    ></v-textarea>
                  </v-col>
                </v-row>
              </v-card>
              <v-col style="margin-top:20px">
              <v-btn v-if="n === 1 ||n === 2  " color="primary" @click="nextStep(n)" > Continue </v-btn>
              <v-btn v-else color="#00db45" @click="click">
                送信
              </v-btn>
              </v-col>
            </v-stepper-content>
          </v-stepper-items>
        </v-stepper>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      e1: 1,
      steps: 3,
      titile: "はっぴーにゅーいやー",
      message: "あけましておめでとうございます!!",
      url : 'https://online.brother.co.jp/BOL/Handlers/DownloadContents400x400.ashx?id=6db6456c-99b9-4a7c-8011-aac4ef92544f',
      from: "田中",
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
  watch: {
    steps(val) {
      if (this.e1 > val) {
        this.e1 = val;
      }
    },
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
                      text: `${this.titile}`,
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
                    `${this.url}`,
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
                      text: `${this.message}`,
                      weight: "bold",
                      size: "sm",
                      align: "center",
                      margin: "none",
                      wrap: true,
                      contents: [],
                    },
                    {
                      type: "text",
                      text: `${this.from}より`,
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
    nextStep(n) {
      if (n === this.steps) {
        this.e1 = 1;
      } else {
        this.e1 = n + 1;
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
