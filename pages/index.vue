<template>
  <div>
    <v-container>
      <div class="mt-8 mt-md-0">
        <div class="d-flex justify-center">
          <div class="card-chat">
            <!-- Chat header -->
            <div class="chat-header text-center">
              <p class="text-16 height-24 font-weight-medium mb-0">
                {{ name }}
              </p>
            </div>
            <!-- Chat body message -->
            <div class="chat-body pos-relative">
              <div v-for="(data, i) in dataUsers" :key="i">
                <!-- Data chat -->
                <div
                  class="d-flex py-2 border-bottom px-2 justify-space-between pointer"
                  @click="chooseUser(data.id)"
                >
                  <div class="d-flex">
                    <v-img
                      :src="require('~/assets/images/avatar/user.png')"
                      class="rounded-cicle mr-2 align-self-center"
                      aspect-ratio="1/1"
                      width="50px"
                      height="50px"
                      max-width="50px"
                      max-height="50px"
                      contain
                    ></v-img>
                    <div class="align-self-center">
                      <p
                        class="font-weight-medium text-16 mb-1 text-ellipsis"
                        style="max-width: 240px"
                      >
                        {{ data.user }}
                      </p>
                      <p
                        class="text-14 blackgrey--text mb-0 text-ellipsis"
                        style="max-width: 240px"
                      >
                        {{ data.chat }}
                      </p>
                    </div>
                  </div>
                  <span class="text-12 grey--text pt-1">{{ data.time }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </v-container>
  </div>
</template>

<script>
export default {
  name: 'ChatListPage',
  layout: 'empty',
  data() {
    return {
      name: 'Choose User',
      dataUsers: [
        {
          id: 1,
          user: 'User 1',
        },
        {
          id: 2,
          user: 'User 2',
        },
      ],
    }
  },
  mounted() {
    // this.getUser()
  },
  methods: {
    // getUser() {
    //   const url = '/users'
    //   this.$axios.get(url).then((response) => {
    //     const result = response.data

    //     if (result.data)
    //   })
    // },
    chooseUser(id) {
      localStorage.setItem('chat_user_id', id)
      this.$router.push('/list')
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
  padding: 8px 0 0;
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
