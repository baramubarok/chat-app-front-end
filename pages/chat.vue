<template>
  <div>
    <v-container>
      <div class="mt-8 mt-md-0">
        <div class="d-flex justify-center">
          <div class="card-chat">
            <!-- Chat header -->
            <div class="chat-header text-center">
              <div class="d-flex justify-space-between">
                <v-icon
                  class="px-3 pointer blackgrey--text"
                  @click="$router.push('/list')"
                  >mdi-arrow-left</v-icon
                >
                <p class="text-16 height-24 font-weight-medium mb-0">
                  {{ name }}
                </p>
                <v-icon class="px-3 d-none d-md-block white--text"
                  >mdi-arrow-left</v-icon
                >
              </div>
            </div>
            <!-- Chat body message -->
            <div class="chat-body">
              <!-- <perfect-scrollbar
                ref="mychat"
                :options="{
                  swipeEasing: false,
                  wheelPropagation: false,
                  wheelSpeed: 0.5,
                }"
              > -->
              <div v-for="(data, i) in refreshChat" :key="i">
                <!-- Recieve chat -->
                <div
                  v-for="(receive, x) in data.receive"
                  :key="x"
                  class="d-flex justify-start mb-4"
                >
                  <v-img
                    :src="require('~/assets/images/avatar/user.png')"
                    class="rounded-cicle mr-2 align-self-end"
                    aspect-ratio="1/1"
                    width="32px"
                    height="32px"
                    max-width="32px"
                    max-height="32px"
                    contain
                  ></v-img>
                  <div>
                    <div
                      v-for="(chat, y) in receive.chat"
                      :key="y"
                      class="card-message-receive mb-1"
                      :class="{
                        'rounded-bl-0': y == receive.chat.length - 1,
                      }"
                    >
                      <p
                        class="text-14 height-20 mb-0 message d-flex flex-wrap"
                      >
                        {{ chat }}
                      </p>
                    </div>
                    <p class="text-12 height-16 grey--text mb-0">
                      {{ receive.time }}
                    </p>
                  </div>
                </div>
                <!-- Sent chat -->
                <div v-for="(sent, j) in data.sent" :key="j" class="mb-4">
                  <div>
                    <!-- Chat -->
                    <div class="d-flex justify-end">
                      <div
                        v-for="(chat, k) in sent.chat"
                        :key="k"
                        class="card-message-sent mb-1"
                        :class="{ 'rounded-br-0': k == sent.chat.length - 1 }"
                      >
                        <!-- <textarea
                          :value="chat"
                          type="text"
                          class="flat"
                          flat
                          placeholder="Kirim pesan"
                        ></textarea> -->
                        <p
                          class="text-14 height-20 mb-0 message"
                          v-html="chat"
                        ></p>
                      </div>
                    </div>
                    <!-- Status -->
                    <div class="d-flex justify-end align-content-center">
                      <v-icon
                        class="text-14 height-14 mr-1"
                        :class="{ 'accentblue--text': sent.status == 'seen' }"
                      >
                        {{
                          sent.status == 'sent' ? 'mdi-check' : 'mdi-check-all'
                        }}
                      </v-icon>

                      <p class="text-12 height-14 grey--text mb-0">
                        {{ sent.time }}
                      </p>
                    </div>
                  </div>
                </div>
              </div>
              <!-- </perfect-scrollbar> -->
            </div>
            <!-- Chat input message -->
            <div class="send-message">
              <div
                class="d-flex align-content-center justify-space-between py-2 px-4"
              >
                <v-menu top offset-x :close-on-content-click="false">
                  <template #activator="{ on, attrs }">
                    <v-icon
                      class="text-27 pointer height-26"
                      v-bind="attrs"
                      :ripple="false"
                      v-on="on"
                      >mdi-emoticon-outline</v-icon
                    >
                  </template>

                  <div class="white pb-4 pl-4">
                    <v-tabs v-model="emojiTab" centered hide-slider>
                      <v-tab
                        v-for="(data, i) in dataEmoji"
                        :key="i"
                        class="tab-emoji"
                      >
                        <p class="text-14 mb-0">{{ data.emoji[0] }}</p>
                      </v-tab>
                    </v-tabs>
                    <v-tabs-items v-model="emojiTab">
                      <v-tab-item v-for="(data, y) in dataEmoji" :key="y">
                        <div class="d-flex flex-wrap emoji-tab-content">
                          <p
                            v-for="(emoji, x) in data.emoji"
                            :key="x"
                            class="mx-1 mb-2 pointer"
                            @click="addEmoji(emoji)"
                          >
                            {{ emoji }}
                          </p>
                        </div>
                      </v-tab-item>
                    </v-tabs-items>
                  </div>
                </v-menu>

                <textarea
                  v-model="msg"
                  type="text"
                  class="input-messages"
                  placeholder="Kirim pesan"
                  @keydown="chatHandler"
                ></textarea>
                <v-icon class="text-27 pointer" @click="sendMessage(msg)"
                  >mdi-arrow-right-bold-circle</v-icon
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </v-container>
  </div>
</template>

<script>
// import { PerfectScrollbar } from 'vue2-perfect-scrollbar'
export default {
  name: 'ChatPage',
  // components: { PerfectScrollbar },
  layout: 'empty',
  data() {
    return {
      msg: '',
      name: 'Pengawas 1',
      emojiTab: null,
      dataChats: [
        {
          receive: [
            {
              time: '12.00',
              chat: ['tes'],
            },
          ],
        },
      ],
      dataEmoji: [
        {
          name: 'people',
          emoji: [
            '😄',
            '😃',
            '😀',
            '😊',
            '😉',
            '😍',
            '😘',
            '😚',
            '😗',
            '😙',
            '😜',
            '😝',
            '😛',
            '😳',
            '😁',
            '😔',
            '😌',
            '😒',
            '😞',
            '😣',
            '😢',
            '😂',
            '😭',
            '😪',
            '😥',
            '😰',
            '😅',
            '😓',
            '😩',
            '😫',
            '😨',
            '😱',
            '😠',
            '😡',
            '😤',
            '😖',
            '😆',
            '😋',
            '😷',
            '😎',
            '😴',
            '😵',
            '😲',
            '😟',
            '😦',
            '😧',
            '👿',
            '😮',
            '😬',
            '😐',
            '😕',
            '😯',
            '😏',
            '😑',
            '👲',
            '👳',
            '👮',
            '👷',
            '💂',
            '👶',
            '👦',
            '👧',
            '👨',
            '👩',
            '👴',
            '👵',
            '👱',
            '👼',
            '👸',
            '😺',
            '😸',
            '😻',
            '😽',
            '😼',
            '🙀',
            '😿',
            '😹',
            '😾',
            '👹',
            '👺',
            '🙈',
            '🙉',
            '🙊',
            '💀',
            '👽',
            '💩',
            '🔥',
            '✨',
            '🌟',
            '💫',
            '💥',
            '💢',
            '💦',
            '💧',
            '💤',
            '💨',
            '👂',
            '👀',
            '👃',
            '👅',
            '👄',
            '👍',
            '👎',
            '👌',
            '👊',
            '✊',
            '👋',
            '✋',
            '👐',
            '👆',
            '👇',
            '👉',
            '👈',
            '🙌',
            '🙏',
            '👏',
            '💪',
            '🚶',
            '🏃',
            '💃',
            '👫',
            '👪',
            '💏',
            '💑',
            '👯',
            '🙆',
            '🙅',
            '💁',
            '🙋',
            '💆',
            '💇',
            '💅',
            '👰',
            '🙎',
            '🙍',
            '🙇',
            '🎩',
            '👑',
            '👒',
            '👟',
            '👞',
            '👡',
            '👠',
            '👢',
            '👕',
            '👔',
            '👚',
            '👗',
            '🎽',
            '👖',
            '👘',
            '👙',
            '💼',
            '👜',
            '👝',
            '👛',
            '👓',
            '🎀',
            '🌂',
            '💄',
            '💛',
            '💙',
            '💜',
            '💚',
            '💔',
            '💗',
            '💓',
            '💕',
            '💖',
            '💞',
            '💘',
            '💌',
            '💋',
            '💍',
            '💎',
            '👤',
            '💬',
            '👣',
          ],
        },
        {
          name: 'nature',
          emoji: [
            '🐶',
            '🐺',
            '🐱',
            '🐭',
            '🐹',
            '🐰',
            '🐸',
            '🐯',
            '🐨',
            '🐻',
            '🐷',
            '🐽',
            '🐮',
            '🐗',
            '🐵',
            '🐒',
            '🐴',
            '🐑',
            '🐘',
            '🐼',
            '🐧',
            '🐦',
            '🐤',
            '🐥',
            '🐣',
            '🐔',
            '🐍',
            '🐢',
            '🐛',
            '🐝',
            '🐜',
            '🐞',
            '🐌',
            '🐙',
            '🐚',
            '🐠',
            '🐟',
            '🐬',
            '🐳',
            '🐎',
            '🐲',
            '🐡',
            '🐫',
            '🐩',
            '🐾',
            '💐',
            '🌸',
            '🌷',
            '🍀',
            '🌹',
            '🌻',
            '🌺',
            '🍁',
            '🍃',
            '🍂',
            '🌿',
            '🌾',
            '🍄',
            '🌵',
            '🌴',
            '🌰',
            '🌱',
            '🌼',
            '🌑',
            '🌓',
            '🌔',
            '🌕',
            '🌛',
            '🌙',
            '🌏',
            '🌋',
            '🌌',
            '🌠',
            '⛅',
            '⛄',
            '🌀',
            '🌁',
            '🌈',
            '🌊',
          ],
        },
        {
          name: 'object',
          emoji: [
            '🎍',
            '💝',
            '🎎',
            '🎒',
            '🎓',
            '🎏',
            '🎆',
            '🎇',
            '🎐',
            '🎑',
            '🎃',
            '👻',
            '🎅',
            '🎄',
            '🎁',
            '🎋',
            '🎉',
            '🎊',
            '🎈',
            '🎌',
            '🔮',
            '🎥',
            '📷',
            '📹',
            '📼',
            '💿',
            '📀',
            '💽',
            '💾',
            '💻',
            '📱',
            '📞',
            '📟',
            '📠',
            '📡',
            '📺',
            '📻',
            '🔊',
            '🔔',
            '📢',
            '📣',
            '⏳',
            '⌛',
            '⏰',
            '⌚',
            '🔓',
            '🔒',
            '🔏',
            '🔐',
            '🔑',
            '🔎',
            '💡',
            '🔦',
            '🔌',
            '🔋',
            '🔍',
            '🛀',
            '🚽',
            '🔧',
            '🔩',
            '🔨',
            '🚪',
            '🚬',
            '💣',
            '🔫',
            '🔪',
            '💊',
            '💉',
            '💰',
            '💴',
            '💵',
            '💳',
            '💸',
            '📲',
            '📧',
            '📥',
            '📤',
            '📩',
            '📨',
            '📫',
            '📪',
            '📮',
            '📦',
            '📝',
            '📄',
            '📃',
            '📑',
            '📊',
            '📈',
            '📉',
            '📜',
            '📋',
            '📅',
            '📆',
            '📇',
            '📁',
            '📂',
            '📌',
            '📎',
            '📏',
            '📐',
            '📕',
            '📗',
            '📘',
            '📙',
            '📓',
            '📔',
            '📒',
            '📚',
            '📖',
            '🔖',
            '📛',
            '📰',
            '🎨',
            '🎬',
            '🎤',
            '🎧',
            '🎼',
            '🎵',
            '🎶',
            '🎹',
            '🎻',
            '🎺',
            '🎷',
            '🎸',
            '👾',
            '🎮',
            '🃏',
            '🎴',
            '🀄',
            '🎲',
            '🎯',
            '🏈',
            '🏀',
            '⚽',
            '⚾',
            '🎾',
            '🎱',
            '🎳',
            '⛳',
            '🏁',
            '🏆',
            '🎿',
            '🏂',
            '🏊',
            '🏄',
            '🎣',
            '🍵',
            '🍶',
            '🍺',
            '🍻',
            '🍸',
            '🍹',
            '🍷',
            '🍴',
            '🍕',
            '🍔',
            '🍟',
            '🍗',
            '🍖',
            '🍝',
            '🍛',
            '🍤',
            '🍱',
            '🍣',
            '🍥',
            '🍙',
            '🍘',
            '🍚',
            '🍜',
            '🍲',
            '🍢',
            '🍡',
            '🍳',
            '🍞',
            '🍩',
            '🍮',
            '🍦',
            '🍨',
            '🍧',
            '🎂',
            '🍰',
            '🍪',
            '🍫',
            '🍬',
            '🍭',
            '🍯',
            '🍎',
            '🍏',
            '🍊',
            '🍒',
            '🍇',
            '🍉',
            '🍓',
            '🍑',
            '🍈',
            '🍌',
            '🍍',
            '🍠',
            '🍆',
            '🍅',
            '🌽',
          ],
        },
        {
          name: 'place',
          emoji: [
            '🏠',
            '🏡',
            '🏫',
            '🏢',
            '🏣',
            '🏥',
            '🏦',
            '🏪',
            '🏩',
            '🏨',
            '💒',
            '⛪',
            '🏬',
            '🌇',
            '🌆',
            '🏯',
            '🏰',
            '⛺',
            '🏭',
            '🗼',
            '🗾',
            '🗻',
            '🌄',
            '🌅',
            '🌃',
            '🗽',
            '🌉',
            '🎠',
            '🎡',
            '⛲',
            '🎢',
            '🚢',
            '⛵',
            '🚤',
            '🚀',
            '💺',
            '🚉',
            '🚄',
            '🚅🚇',
            '🚃',
            '🚌',
            '🚙',
            '🚗',
            '🚕',
            '🚚',
            '🚨',
            '🚓',
            '🚒',
            '🚑',
            '🚲',
            '💈',
            '🚏',
            '🎫',
            '🚥',
            '🚧',
            '🔰',
            '⛽',
            '🏮',
            '🎰',
            '🗿',
            '🎪',
            '🎭',
            '📍',
            '🚩',
          ],
        },
        {
          name: 'symbol',
          emoji: [
            '💯',
            '🔢',
            '🔟',
            '🔣',
            '🔠',
            '🔡',
            '🔤',
            '🔼',
            '🔽',
            '⏪',
            '⏩',
            '⏫',
            '⏬',
            '🆗',
            '🆕',
            '🆙',
            '🆒',
            '🆓',
            '🆖',
            '📶',
            '🎦',
            '🈁',
            '🈯',
            '🈳',
            '🈵',
            '🈴',
            '🈲',
            '🉐',
            '🈹',
            '🈺',
            '🈶',
            '🈚',
            '🚻',
            '🚹',
            '🚺',
            '🚼',
            '🚾',
            '🚭',
            '🈸',
            '🉑',
            '🆑',
            '🆘',
            '🆔',
            '🚫',
            '🔞',
            '⛔',
            '❎',
            '✅',
            '💟',
            '🆚',
            '📳',
            '📴',
            '🆎',
            '💠',
            '⛎',
            '🔯',
            '🏧',
            '💹',
            '💲',
            '💱',
            '❌',
            '❗',
            '❓',
            '❕',
            '❔',
            '⭕',
            '🔝',
            '🔚',
            '🔙',
            '🔛',
            '🔜',
            '🔃',
            '🕛',
            '🕐',
            '🕑',
            '🕒',
            '🕓',
            '🕔',
            '🕕',
            '🕖',
            '🕗',
            '🕘',
            '🕙',
            '🕚',
            '➕',
            '➖',
            '➗',
            '💮',
            '🔘',
            '🔗',
            '➰',
            '🔱',
            '🔺',
            '🔲',
            '🔳',
            '🔴',
            '🔵',
            '🔻',
            '⬜',
            '⬛',
            '🔶',
            '🔷',
            '🔸',
            '🔹',
          ],
        },
      ],
    }
  },
  computed: {
    refreshChat() {
      return this.dataChats
    },
  },
  mounted() {
    // this.scrollBottom()
    console.log(this.$route.query)
  },
  methods: {
    chatHandler(e) {
      if (e.keyCode === 13 && !e.shiftKey) {
        e.preventDefault()
        this.sendMessage(this.msg)
      }
    },
    scrollBottom() {
      const container = this.$el.querySelector('.chat-body')
      container.scrollTop = 1000000000000
    },
    addEmoji(emoji) {
      this.msg += emoji
    },
    sendMessage(chats) {
      chats = chats.replace('\n', '<br>')
      if (chats !== '') {
        const today = new Date()
        const nowTime = today.getHours() + '.' + today.getMinutes()
        const data = {
          sent: [
            {
              time: nowTime,
              status: 'sent',
              chat: [chats],
            },
          ],
        }
        this.dataChats.push(data)
        setTimeout(this.scrollBottom, 100)
        this.msg = ''
      }
    },
  },
}
</script>

<style scoped>
@import '~/assets/styles.css';

.card-chat {
  width: 360px;
  height: 600px;
  background: #fcfcfc;
  border: 2px solid #dba11c;
  box-shadow: 2px 0px 29px rgba(0, 0, 0, 0.09);
  border-radius: 12px;
}
.chat-header {
  padding: 14px 0;
  box-shadow: 0px 1px 0px rgba(0, 0, 0, 0.08);
}
.chat-body {
  padding: 8px;
  height: 488px !important;
  max-height: 488px !important;
  overflow-y: scroll;
}
.chat-body::-webkit-scrollbar-track {
  border-radius: 100px !important;
  background-color: transparent !important;
}
.chat-body::-webkit-scrollbar {
  border-radius: 100px;
  width: 4px !important;
  background-color: transparent !important;
}
.chat-body::-webkit-scrollbar-thumb {
  border-radius: 100px !important;
  background-color: #c4c4c4 !important;
}
.ps {
  height: 480px;
  max-height: 480px !important;
}
div >>> .ps__rail-x {
  display: none !important;
}
div >>> .ps__rail-y {
  display: none !important;
}
.card-message-receive {
  padding: 8px 16px;
  max-width: 272px;
  background: #ffffff;
  border-radius: 16px;
  border: 1px solid #ecebeb;
}
.message {
  white-space: wrap;
  word-break: break-all;
  /* white-space: normal; */
}
.card-message-sent {
  padding: 8px 16px;
  max-width: 272px;
  background: #ecebeb;
  border-radius: 16px;
}
.send-message {
  height: 56px !important;
  background: #ffffff;
  box-shadow: 0px -1px 0px rgba(0, 0, 0, 0.08);
  border-radius: 0 0 12px 12px;
  z-index: 2;
}
.input-messages {
  padding: 10px 16px;
  height: 40px;
  max-height: 40px;
  width: 248px;
  background: #ffffff;
  border: 1px solid #ecebeb;
  border-radius: 20px;
  font-size: 14px;
  line-height: 17px;
  font-weight: 500;
  resize: none;
}
textarea {
  outline: none;
}
div >>> .theme--light.v-icon:focus::after {
  opacity: 0 !important;
}
.tab-emoji {
  min-width: 0px !important;
}
.emoji-tab-content {
  max-width: 260px;
  max-height: 250px;
  overflow-y: scroll;
  box-sizing: content-box;
}
</style>
