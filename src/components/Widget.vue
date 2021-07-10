<script>
import Message from "./Message.vue";
export default {
  components: {
    Message,
  },
  data() {
    return {
      control: false,
      text: null,
    };
  },
  props: {
    companyName: {
      type: String,
      default: "Widget",
    },
    textReply: {
      type: String,
      default: "Typically replies within an hour",
    },
    messages: {
      type: Array,
      default: () => ["Hi there 👋 How can I help you ?"],
    },
    companyLogo: {
      type: String,
      default: "",
    },
    phoneNumber: {
      type: String,
      default: "",
    },
  },
  methods: {
    openLink() {
      let url = "https://web.whatsapp.com/send";
      if (
        /Android|webOS|iPhone|iPad|Mac|Macintosh|iPod|BlackBerry|IEMobile|Opera Mini/i.test(
          navigator.userAgent
        )
      ) {
        url = "whatsapp://send";
      }
      const all = url + "?phone=" + this.phoneNumber + `&text=${this.text}`;
      window.open(all, "_blank");
    },
  },
};
</script>
<template>
  <div id="wp-widget">
    <div v-if="control" id="whatsapp-chat" class="hidden">
      <div class="whatsapp-chat-header">
        <div class="whatsapp-chat-avatar">
          <img
            v-if="companyLogo"
            :src="companyLogo"
            :alt="companyName + ' ' + 'Logo'"
          />
          <div v-else class="companyLogo"></div>
        </div>
        <p class="whatsapp-chat-name-block">
          <span class="whatsapp-chat-name">{{ companyName }}</span
          ><br /><small>{{ textReply }}</small>
        </p>
      </div>

      <div class="start-chat">
        <div
          pattern="https://elfsight.com/assets/chats/patterns/whatsapp.png"
          class="WhatsappChat__Component-sc-Yvjha whatsapp-chat-body"
        >
          <Message :messages="messages" />
        </div>

        <div class="blanter-msg">
          <textarea
            id="chat-input"
            placeholder="Write a response"
            maxlength="120"
            row="1"
            v-model="text"
          ></textarea>
          <button id="send-it" @click="openLink">
            <svg viewBox="0 0 448 448">
              <path d="M.213 32L0 181.333 320 224 0 266.667.213 416 448 224z" />
            </svg>
          </button>
        </div>
      </div>
      <a class="close-chat" @click="control = false">×</a>
    </div>
    <button
      class="blantershow-chat"
      title="Start Chat"
      @click="control = !control"
    >
      <svg width="30" viewBox="0 0 24 24">
        <defs />
        <path
          fill="#eceff1"
          d="M20.5 3.4A12.1 12.1 0 0012 0 12 12 0 001.7 17.8L0 24l6.3-1.7c2.8 1.5 5 1.4 5.8 1.5a12 12 0 008.4-20.3z"
        />
        <path
          fill="#4caf50"
          d="M12 21.8c-3.1 0-5.2-1.6-5.4-1.6l-3.7 1 1-3.7-.3-.4A9.9 9.9 0 012.1 12a10 10 0 0117-7 9.9 9.9 0 01-7 16.9z"
        />
        <path
          fill="#fafafa"
          d="M17.5 14.3c-.3 0-1.8-.8-2-.9-.7-.2-.5 0-1.7 1.3-.1.2-.3.2-.6.1s-1.3-.5-2.4-1.5a9 9 0 01-1.7-2c-.3-.6.4-.6 1-1.7l-.1-.5-1-2.2c-.2-.6-.4-.5-.6-.5-.6 0-1 0-1.4.3-1.6 1.8-1.2 3.6.2 5.6 2.7 3.5 4.2 4.2 6.8 5 .7.3 1.4.3 1.9.2.6 0 1.7-.7 2-1.4.3-.7.3-1.3.2-1.4-.1-.2-.3-.3-.6-.4z"
        />
      </svg>
    </button>
  </div>
</template>
<style lang="scss">
button {
  outline: none;
}
#wp-widget {
  font-family: --system-ui, "Lato", sans-serif;
  background: #f1f1f1;
}
a:link,
a:visited {
  color: #444;
  text-decoration: none;
  transition: all 0.4s ease-in-out;
}
h1 {
  font-size: 20px;
  text-align: center;
  display: block;
  background: linear-gradient(to right top, #6f96f3, #164ed2);
  padding: 20px;
  color: #fff;
  border-radius: 50px;
}

/* CSS Multiple Whatsapp Chat */

#whatsapp-chat {
  box-sizing: border-box !important;
  outline: none !important;
  position: fixed;
  width: 350px;
  border-radius: 10px;
  box-shadow: 0 1px 15px rgba(32, 33, 36, 0.28);
  bottom: 90px;
  right: 30px;
  overflow: hidden;
  z-index: 99;
  animation-name: showchat;
  animation-duration: 1s;
  transform: scale(1);
}

button.blantershow-chat {
  /*   background: #009688; */
  background: #fff;
  color: #404040;
  position: fixed;
  display: flex;
  font-weight: 400;
  justify-content: space-between;
  z-index: 98;
  bottom: 25px;
  right: 30px;
  font-size: 15px;
  padding: 15px 15px;
  border-radius: 50%;
  border: 1px solid transparent;
  box-shadow: 0 10px 10px rgba(32, 33, 36, 0.28);
  cursor: pointer;
}

button.blantershow-chat svg {
  transform: scale(1.2);
}

.whatsapp-chat-header {
  background: #095e54;
  display: inline-flex;
  align-items: center;
  padding-left: 10px;
  height: 60px;
  width: 100%;
  height: 100%;
  color: #fff;
}
.companyLogo {
  border-radius: 100%;
  width: 50px;
  height: 50px;
  float: left;
  margin: 0 10px 0 0;
  border: 1px solid rgba(black, 0.2);
}
.whatsapp-chat-avatar {
  position: relative;
  &::after {
    content: "";
    bottom: 0px;
    right: 0px;
    width: 12px;
    height: 12px;
    box-sizing: border-box;
    background-color: #4ad504;
    display: block;
    position: relative;
    z-index: 1;
    border-radius: 50%;
    border: 2px solid #095e54;
    left: 40px;
    top: 38px;
  }
  img {
    border-radius: 100%;
    width: 50px;
    float: left;
    margin: 0 10px 0 0;
  }
}
.whatsapp-chat-name-block {
  text-align: left;
}
.info-chat span {
  display: block;
}
#get-label,
span.chat-label {
  font-size: 12px;
  color: #888;
}
#get-nama,
span.chat-nama {
  margin: 5px 0 0;
  font-size: 15px;
  font-weight: 700;
  color: #222;
}
#get-label,
#get-nama {
  color: #fff;
}
span.my-number {
  display: block;
}
/* .blanter-msg {
  color: #444;
  padding: 20px;
  font-size: 12.5px;
  text-align: center;
  border-top: 1px solid #ddd;
} */
textarea#chat-input {
  border: none;
  font-family: "Arial", sans-serif;
  width: 100%;
  outline: none;
  resize: none;
  padding: 8px;
  font-size: 14px;
}

button#send-it {
  width: 30px;
  font-weight: 700;
  border-color: transparent;
  cursor: pointer;
  background: #eee;

  svg {
    fill: #a6a6a6;
    height: 20px;
    width: 20px;
  }
}

.start-chat .blanter-msg {
  display: flex;
  height: 35px;
}
a.close-chat {
  position: absolute;
  top: 5px;
  right: 15px;
  color: #fff;
  font-size: 30px;
  cursor: pointer;
}

@keyframes ZpjSY {
  0% {
    background-color: rgb(182, 181, 186);
  }
  15% {
    background-color: rgb(17, 17, 17);
  }
  25% {
    background-color: rgb(182, 181, 186);
  }
}

@keyframes hPhMsj {
  15% {
    background-color: rgb(182, 181, 186);
  }
  25% {
    background-color: rgb(17, 17, 17);
  }
  35% {
    background-color: rgb(182, 181, 186);
  }
}

@keyframes iUMejp {
  25% {
    background-color: rgb(182, 181, 186);
  }
  35% {
    background-color: rgb(17, 17, 17);
  }
  45% {
    background-color: rgb(182, 181, 186);
  }
}

@keyframes showhidden {
  from {
    transform: scale(0.5);
    opacity: 0;
  }
}
@keyframes showchat {
  from {
    transform: scale(0);
    opacity: 0;
  }
}
@media screen and (max-width: 480px) {
  #whatsapp-chat {
    width: auto;
    left: 5%;
    right: 5%;
    font-size: 80%;
  }
}
.hidden {
  display: block;
  animation-duration: 0.5s;
  transform: scale(1);
  opacity: 1;
}
.show {
  display: block;
  animation-name: showhidden;
  animation-duration: 0.5s;
  transform: scale(1);
  opacity: 1;
}

.whatsapp-chat-body {
  padding: 20px 20px 20px 10px;
  background-color: rgb(230, 221, 212);
  position: relative;
  &::before {
    display: block;
    position: absolute;
    content: "";
    left: 0px;
    top: 0px;
    height: 100%;
    width: 100%;
    z-index: 0;
    opacity: 0.08;
    background-image: url("https://elfsight.com/assets/chats/patterns/whatsapp.png");
    // background-image: url(https://res.cloudinary.com/eventbree/image/upload/v1575782560/Widgets/whatsappbg_opt.jpg);
  }
}

.quaMo {
  z-index: 1;
}

.vzZsj {
  background-color: rgb(255, 255, 255);
  width: 52.5px;
  border-radius: 16px;
  display: flex;
  -moz-box-pack: center;
  justify-content: center;
  -moz-box-align: center;
  align-items: center;
  margin-left: 10px;
  opacity: 0;
  transition: all 0.1s ease 0s;
  z-index: 1;
  box-shadow: rgba(0, 0, 0, 0.13) 0px 1px 0.5px;
}

.Yvjha {
  position: relative;
  display: flex;
}

.ixsrax {
  height: 5px;
  width: 5px;
  margin: 0px 2px;
  border-radius: 50%;
  display: inline-block;
  position: relative;
  animation-duration: 1.2s;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
  top: 0px;
  background-color: rgb(158, 157, 162);
  animation-name: ZpjSY;
}

.dRvxoz {
  height: 5px;
  width: 5px;
  margin: 0px 2px;
  background-color: rgb(182, 181, 186);
  border-radius: 50%;
  display: inline-block;
  position: relative;
  animation-duration: 1.2s;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
  top: 0px;
  animation-name: hPhMsj;
}

.kAZgZq {
  padding: 7px 14px 6px;
  background-color: rgb(255, 255, 255);
  border-radius: 0px 12px 12px;
  position: relative;
  transition: all 0.3s ease 0s;
  opacity: 0;
  transform-origin: center top 0px;
  z-index: 2;
  box-shadow: rgba(0, 0, 0, 0.13) 0px 1px 0.5px;
  margin-top: 20px;
  max-width: calc(100% - 66px);
  &::before {
    position: absolute;
    background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAmCAMAAADp2asXAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAACQUExURUxpccPDw9ra2m9vbwAAAAAAADExMf///wAAABoaGk9PT7q6uqurqwsLCycnJz4+PtDQ0JycnIyMjPf3915eXvz8/E9PT/39/RMTE4CAgAAAAJqamv////////r6+u/v7yUlJeXl5f///5ycnOXl5XNzc/Hx8f///xUVFf///+zs7P///+bm5gAAAM7Ozv///2fVensAAAAvdFJOUwCow1cBCCnqAhNAnY0WIDW2f2/hSeo99g1lBYT87vDXG8/6d8oL4sgM5szrkgl660OiZwAAAHRJREFUKM/ty7cSggAABNFVUQFzwizmjPz/39k4YuFWtm55bw7eHR6ny63+alnswT3/rIDzUSC7CrAziPYCJCsB+gbVkgDtVIDh+DsE9OTBpCtAbSBAZSEQNgWIygJ0RgJMDWYNAdYbAeKtAHODlkHIv997AkLqIVOXVU84AAAAAElFTkSuQmCC");
    background-position: 50% 50%;
    background-repeat: no-repeat;
    background-size: contain;
    content: "";
    top: 0px;
    left: -12px;
    width: 12px;
    height: 19px;
  }
}

.bMIBDo {
  font-size: 13px;
  font-weight: 700;
  line-height: 18px;
  text-align: left;
  color: rgba(0, 0, 0, 0.4);
}

.iSpIQi {
  font-size: 14px;
  line-height: 19px;
  margin-top: 4px;
  color: rgb(17, 17, 17);
  text-align: left;
}

.cqCDVm {
  text-align: right;
  margin-top: 4px;
  font-size: 12px;
  line-height: 16px;
  color: rgba(17, 17, 17, 0.5);
  margin-right: -8px;
  margin-bottom: -4px;
}
</style>
