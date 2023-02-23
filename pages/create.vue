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
            <div class="chat-body px-4">
              <v-form class="d-flex h-100 flex-column justify-space-between">
                <div>
                  <v-text-field
                    outlined
                    placeholder="Name"
                    hide-details
                    dense
                    class="mb-3 text-14"
                  ></v-text-field>
                  <v-textarea
                    v-model="message"
                    outlined
                    placeholder="Message"
                    class="mb-3 text-14"
                    hide-details
                  ></v-textarea>
                </div>
                <div>
                  <v-btn block class="rounded-8" color="primary">Send</v-btn>
                </div>
              </v-form>
            </div>
          </div>
        </div>
      </div>
    </v-container>
  </div>
</template>

<script>
export default {
  name: 'CreateChatPage',
  layout: 'empty',
  data() {
    return {
      name: 'Create Chat',
      username: null,
      message: null,
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
      const container = this.$el.querySelector('.ps')
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
  height: 540px !important;
  max-height: 540px !important;
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
  height: 530px;
  max-height: 530px !important;
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
