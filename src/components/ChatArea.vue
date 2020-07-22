<template>
  <div>
    <div class="fabs">
      <div class="chat" v-if="!isMessage">
        <div class="chat_header">
          <div class="chat_option">
            <div id="chat_head">Hi There</div>

            <div class="sub">{{ subheading}}</div>
          </div>
        </div>
        <div class="chat-body">
          <h6 class="conversation">{{ conversation }}</h6>
          <p>{{ discription }}</p>
        </div>

        <div class="chat-box-list-container" ref="chatbox">
          <ul class="chat-box-list">
            <li
              class="message"
              v-for="(message, idx) in messages"
              :key="idx"
              :class="message.author"
            >
              <p class="server-mess">
                <span class="ser-message">{{ message.text }}</span>
              </p>
            </li>
          </ul>
        </div>
        <div class="bottomIcon" v-if="!isIcon">
          <div class="sparrow-icon"></div>
          <span>We run on surveysparrow</span>
        </div>
        <div class="fab_field">
          <input type="text" v-model="message" :placeholder="[[ placeholder ]]" />

          <button @click="sendMessage" :disabled="message === ''">
            <i class="material-icons">send</i>
          </button>
        </div>
      </div>
      <div id="chat-icon">
        <div @click="toggleBox" :class="{ icon: isActive , icon1 : isShow } "></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "ChatBox",

  data: () => ({
    subheading: "Ask Us Anything, Share Your Feedback",
    discription: "The team replies in few a minutes ",
    conversation: "Start a Conversation",
    placeholder: "New Coversation",
    isMessage: true,
    isActive: true,
    isShow: false,
    isIcon: true,
    message: "",
    messages: []
  }),
  methods: {
    sendMessage(e) {
      e.preventDefault();
      const message = this.message;

      this.messages.push(
        {
          text: message,
          author: "client"
        },
        setInterval
      );

      this.message = "";
      this.subheading = "The team replies in few a Minutes";
      this.discription = "";
      this.conversation = " ";
      this.placeholder = " Write a replay";
      this.isIcon = false;

      this.$axios.get(`https://api.adviceslip.com/advice`).then(res => {
        this.messages.push({
          text: res.data.slip.advice,
          author: "server"
        });
        console.log(res.data.slip.advice);

        this.$nextTick(() => {
          this.$refs.chatbox.scrollTop = this.$refs.chatbox.scrollHeight;
        });
      });
    },
    showBox() {
      this.isMessage = false;
      this.isActive = false;
      this.isShow = true;
    },
    hideBox() {
      this.isMessage = true;
      this.isActive = true;
      this.isShow = false;
    },
    toggleBox() {
      return this.isMessage ? this.showBox() : this.hideBox();
    }
  }
};
</script>

<style lang="scss" scoped>
$blue-violet: "#7F8AC5";
$light-green: "#13A884";
$blue: "#4C5AA1";
$rose-white: "#ECF1FB";
$dark-blue: "#0C003A";
.fabs {
  bottom: 0;
  position: fixed;
  margin: 1em;
  right: 0;
  z-index: 998;
}

/*Chatbox*/

.chat {
  position: fixed;
  background-color: #fff;
  border-radius: 5px;
  right: 45px;
  bottom: 100px;
  width: 400px;
  font-size: 12px;
  line-height: 22px;
  font-weight: 500;
  -webkit-animation: openbox 0.25s ease-out;
  /* Chrome, Safari, Opera */
  animation: openbox 0.25s ease-out;
}
.chat_header {
  /* margin: 10px; */
  font-size: 13px;
  color: #f3f3f3;
  height: 100px;
  background: #7f8ac5;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
}

.chat_option {
  float: left;
  font-size: 16px;
  list-style: none;
  font-weight: 400;
  #chat_head {
    margin-bottom: 20px;
  }
  .sub {
    font-size: 15px;
  }
}
.icon {
  position: absolute;
  transition-delay: 25ms;
  -webkit-transition: 0.6s ease-out;
  -moz-transition: 0.6s ease-out;
  transition: 0.6s ease-out;
}
.icon::before {
  position: absolute;
  content: url("../img/SparrowBird.png");
  object-fit: contain;
  margin-left: 8px;
  top: 1px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
.icon1 {
  position: absolute;
  transition-delay: 25ms;
  -webkit-transition: 0.6s ease-out;
  -moz-transition: 0.6s ease-out;
  transition: 0.6s ease-out;
}
.icon1::before {
  position: absolute;
  content: url("../img/close.svg");
  object-fit: contain;
  width: 30px;
  height: 30px;
  margin-left: 20px;
  top: 20px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
#chat-icon {
  display: block;
  width: 70px;
  height: 70px;
  top: -10px;
  bottom: 0;
  border-radius: 50px 50px 3px 50px;
  text-align: center;
  color: #f0f0f0;
  float: right;
  margin-right: 20px;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.14), 0 4px 8px rgba(0, 0, 0, 0.28);
  cursor: pointer;
  -webkit-transition: all 0.1s ease-out;
  transition: all 0.1s ease-out;
  position: relative;
  z-index: 998;
  overflow: hidden;
  background: #ffffff;
}
ul li {
  list-style: none;
}

.chat-body {
  background: #fff;
  width: 100%;
  display: inline-block;
  text-align: center;
  overflow-y: auto;
  .conversation {
    font-weight: 600;
    font-size: 14px;
  }
}
.chat-box-list-container {
  max-height: 300px;
  overflow: scroll;
  background-color: #ffffff;
  position: relative;
  margin-bottom: 30px;
  .chat-box-list {
    font-size: 12px;
    li {
      position: relative;
      margin: 8px 0 15px 0;
      padding: 8px 10px;
      max-width: 60%;
      display: block;
      clear: both;
    }
    li.message.client {
      position: relative;
      color: #fff;
      margin-right: 20px;
      float: right;
      background: #4c5aa1;
      padding: 10px 15px;
      border-radius: 5px;
    }
    li.message.client::after {
      position: absolute;
      content: "";
      right: 0;
      bottom: -12px;
      width: 0px;
      height: 0px;
      border-radius: 5px;
      border-top: solid 10px #4c5aa1;
      border-right: solid 10px #4c5aa1;
      border-left: solid 10px transparent;
      border-bottom: solid 10px transparent;
    }
    li.message.server {
      margin-left: 50px;
      float: left;
      background: #f1f1f1;
      color: #666;
      position: relative;
    }
    li.message.server::before {
      position: absolute;
      content: "";
      top: 0px;
      left: -30px;
      width: 20px;
      height: 20px;
      background-color: #4c5aa1;
      border-radius: 50%;
    }
    li.message.server::after {
      position: absolute;
      content: "";
      left: 0;
      bottom: -12px;
      width: 0px;
      height: 0px;
      border-radius: 5px;
      border-top: solid 10px #f1f1f1;
      border-left: solid 10px #f1f1f1;
      border-right: solid 10px transparent;
      border-bottom: solid 10px transparent;
    }
  }
}
.bottomIcon {
  position: absolute;
  align-items: center;
  bottom: 55px;
  display: flex;
  margin-left: 90px;
  font-size: 8px;
  color: #999;
}
.sparrow-icon {
  width: 15px;
  height: 15px;
  margin-right: 4px;
  background: url("../img/sparrowfavicon.png");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
// *** fab_field
.fab_field {
  width: 100%;
  display: flex;
  text-align: center;
  background: #fff;

  border-top: 1px solid #eee;
  border-radius: 5px;
  input {
    border: none;
    padding: 15px 10px;
    color: #fff;
    width: 100%;
  }
  input:focus {
    background-color: #fff;
    border: none;
    width: 100%;
    padding: 15px 10px;
    color: #555;
    outline: none;
  }
  button {
    border: none;
    background-color: #fff;
    padding: 0 10px;
    outline: none;
    i {
      color: #7f8ac5;
    }
  }
}

/*Chatbox scrollbar*/

::-webkit-scrollbar {
  width: 6px;
}

::-webkit-scrollbar-track {
  border-radius: 0;
}

::-webkit-scrollbar-thumb {
  margin: 2px;
  border-radius: 10px;
  background: rgba(0, 0, 0, 0.2);
}

/* animations to expand boxChrome, Safari, Opera */

@-webkit-keyframes openbox {
  0% {
    height: 0px;
    width: 0px;
  }
  100% {
    width: 350px;
  }
}

@keyframes openbox {
  0% {
    height: 0px;
    width: 0px;
  }
  100% {
    width: 350px;
  }
}

/* SMARTPHONES PORTRAIT */

@media only screen and (min-width: 300px) {
  .chat {
    width: 250px;
  }
}
/* SMARTPHONES LANDSCAPE */

@media only screen and (min-width: 480px) {
  .chat {
    width: 300px;
  }
  .chat_field {
    width: 65%;
  }
}
/* TABLETS PORTRAIT */

@media only screen and (min-width: 768px) {
  .chat {
    width: 300px;
  }
  .chat_field {
    width: 65%;
  }
}
/* TABLET LANDSCAPE / DESKTOP */

@media only screen and (min-width: 1024px) {
  .chat {
    width: 350px;
  }
  .chat_field {
    width: 65%;
  }
}

::-webkit-input-placeholder {
  /* Chrome */
  color: #bbb;
}
:-ms-input-placeholder {
  /* IE 10+ */
  color: #bbb;
}
::-moz-placeholder {
  /* Firefox 19+ */
  color: #bbb;
}
:-moz-placeholder {
  /* Firefox 4 - 18 */
  color: #bbb;
}
</style>