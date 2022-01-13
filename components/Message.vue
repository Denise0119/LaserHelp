<template>
  <div class="bg-gray-100 pb-10">
    <div class="grid grid-cols-10 gap-2">
      <div
        class="col-start-1 col-end-1 bg-white mt-4 mx-4 rounded-md"
        :class="is_shown ? 'hide_sidebar' : ''"
      >
        <p
          class="cursor-pointer py-40 font-bold text-xl flex justify-center"
          @click="show"
        >
          show
        </p>
      </div>
      <div
        class="col-start-1 col-end-3 bg-white mt-4 mx-4 rounded-md"
        :class="is_shown ? '' : 'hide_sidebar'"
      >
        <div class="flex justify-between cursor-pointer">
          <p class="font-bold text-lg px-2">Contacts</p>
          <p class="font-semibold text-base px-2" id="kk" @click="hide">Hide</p>
        </div>
        <div
          class="
            flex
            mt-3
            px-3
            justify-between
            items-center
            bg-gray-200
            cursor-pointer
          "
        >
          <div class="flex items-center py-2">
            <img src="../assets/avatar.jpg" alt="" class="rounded-full w-8" />
            <p class="mx-2">
              {{ receiver.firstname + " " + receiver.lastname }}
            </p>
          </div>
          <p class="text-sm text-gray-700">10:16 PM</p>
        </div>
        <div style="height: 700px"></div>
      </div>
      <div
        class="col-start-3 col-end-6 bg-white mt-4 rounded-md"
        :class="is_shown ? '' : 'large_side'"
      >
        <div class="flex justify-between px-3 items-center pt-3">
          <div class="text-center">
            <span class="text-2xl font-bold text-center">{{
              receiver.firstname + " " + receiver.lastname
            }}</span>
          </div>
          <div class="flex justify-center items-center">
            <div class="cursor-pointer mr-4">
              <img src="../assets/CHAT.png" class="w-6" />
            </div>
            <div class="cursor-pointer justify-center items-center">
              <img src="../assets/PHONE.png" class="w-6" />
            </div>
          </div>
        </div>
        <div class="mt-3 flex items-center justify-start w-full px-2">
          <select
            class="
              text-center text-xs
              h-6
              pl-2
              pr-2
              placeholder-gray-600
              border
              rounded-lg
            "
          >
            <option>I am service provider</option>
            <option>I am client</option>
          </select>
        </div>
        <div>
          <div class="flex justify-center">
            <p class="text-gray-500 text-sm mx-10 mt-5">
              Lendon missed your call, please try again in a moment or wait for
              him to call back
            </p>
          </div>
        </div>
        <!-- <div style="background: red; width: 200px; height: 200px">
          {{ messages }}
        </div> -->
        <div
          v-if="
            isExpert !== 1 &&
            acceptedstate.accept == 'accept' &&
            acceptedstate.chat == 'yes'
          "
          class="
            float-left
            w-full
            justify-between
            items-center
            text-center text-neutral-500
            py-3
            font-sans font-semibold
          "
        >
          Live chat has started
        </div>
        <div style="height: 600px" class="items-baseline">
          <div
            v-for="item in messages"
            :key="item"
            class="w-8/12 mt-2 px-2 py-2 rounded-md"
            :class="
              item.userid == curID
                ? 'bg-yellow-200 float-right text-left mt-10'
                : 'bg-blue-200 float-left text-left'
            "
          >
            <!-- </div> -->
            <span>{{ item.message }}</span>
            <!-- <img
              class="rounded-full float-right w-10 h-10"
              src="../assets/myphoto.jpg"
              alt="Lendon"
            /> -->
          </div>
          <div
            v-if="
              isExpert !== 1 &&
              acceptedstate.accept !== 'accept' &&
              !isCustomsAccepted &&
              firstshow
            "
            class="
              float-left
              w-full
              justify-between
              items-center
              text-center text-neutral-500
              py-3
              font-sans font-semibold
            "
          >
            Waiting for Expert to accept this question...
          </div>
          <div
            v-if="
              isExpert !== 1 &&
              acceptedstate.accept == 'accept' &&
              acceptedstate.chat == 'no'
            "
            class="
              float-left
              w-full
              justify-between
              items-center
              text-center text-neutral-500
              py-3
              font-sans font-semibold
            "
          >
            Expert accepted your question....
          </div>

          <div
            v-if="
              isExpert == 1 &&
              acceptedstate.accept !== 'accept' &&
              acceptedstate.accept != null
            "
            class="
              w-full
              mt-2
              px-2
              py-2
              rounded-md
              flex flex-inline
              relative
              justify-center
              space-x-4
              items-center
              p-2
            "
          >
            <button
              class="bg-[#059669] text-black w-150 h-30 p-2 rounded-3xl"
              :class="is_shown_buttons ? '' : 'hide_buttons'"
              @click="hideADButtons"
            >
              Accept question
            </button>
            <button
              class="bg-[#e11d48] text-black w-150 h-30 p-2 rounded-3xl"
              :class="is_shown_buttons ? '' : 'hide_buttons'"
              @click="hideDAButtons"
            >
              Decline question
            </button>
          </div>
          <div
            v-if="
              isExpert == 1 &&
              !isCustomsAccepted &&
              acceptedstate.accept == 'accept'
            "
            class="
              w-full
              mt-2
              px-2
              py-2
              rounded-md
              flex flex-inline
              relative
              justify-center
              space-x-4
              items-center
              p-2
            "
          >
            Wait for customer to begin live chat or call!
          </div>
          <div
            v-if="acceptedstate.accept == 'accept'"
            class="
              w-full
              mt-2
              px-2
              py-2
              rounded-md
              flex flex-inline
              relative
              justify-center
              space-x-4
              items-center
              p-2
            "
            :class="isActive ? 'started-chat' : ''"
          >
            <div
              class="border-2 border-gray-500 mx-2 rounded-md cursor-pointer"
            >
              <div class="flex justify-between px-4 py-1 items-center">
                <span class="pr-2 text-md">Begin the Call</span>
                <img src="../assets/PHONE.png" class="h-6" />
              </div>
            </div>

            <div class="border-2 border-gray-500 rounded-md cursor-pointer">
              <div class="flex justify-between px-4 py-1 items-center">
                <span
                  class="pr-2 text-md"
                  v-if="isActive === false"
                  @click="startChatTimer"
                  >Begin the Chat
                </span>
                <img src="../assets/CHAT.png" class="h-6" />
              </div>
            </div>
          </div>
        </div>
        <div class="flex mx-4 my-3 justify-between items-center">
          <input
            type="text"
            v-model="curMsg"
            v-on:keyup.enter="sendMsg"
            class="
              font-xs
              border-2 border-gray-300
              w-full
              rounded-md
              h-10
              bg-gray-100
              focus:outline-none
            "
            placeholder="Call Lendon or begin Live Chatting to continue the conversation."
          />
          <img src="../assets/send.png" class="w-8 h-8" @click="sendMsg" />
        </div>
      </div>
      <div class="col-start-7 col-end-9 mt-4 rounded-md h-12">
        <div
          class="
            border-2 border-gray-500
            bg-white
            h-12
            rounded-md
            cursor-pointer
            float-right
          "
          :class="isActive ? 'show-end-chat-button' : 'hide-end-chat-button'"
          style="width: 180px !important"
        >
          <div class="flex justify-center px-4 py-1 items-center">
            <span class="pr-2 text-md" @click="endChatTimer">End the Chat</span>
            <img src="../assets/CHAT.png" class="h-6" />
          </div>
        </div>
      </div>
      <div
        class="chat-timer col-start-9 col-end-10 h-12 bg-white mt-4 rounded-md"
      >
        <div class="time-tile">Chat Time:</div>
        <div>{{ hour }}:{{ minute }}:{{ second }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
let pre_curID;
let isExpert = 0;

// const db = firestore;

// const baseURL = process.env.VUE_APP_BASE_URL;
const baseURL = "https://laserhelp-server.herokuapp.com";

export default {
  data() {
    return {
      isActive: false,
      firstshow: false,
      isCustomsAccepted: false,
      disabled: 0,
      timerType: 0,
      hasChatStarted: false,
      alert_message: "",
      totalSeconds: 0 * 60,
      pomodoroInstance: null,
      is_shown: true,
      isExpert: 0,
      arry: true,
      isAccept: null,
      is_shown_buttons: false,
      messages: [],
      curMsg: "",
      receiver: "null",
      acceptedstate: [],
      user: this.$store.state.localStorage.user,
      // recv_id: this.$store.state.localStorage.user.id,
      recv_id: this.$route.params.id,
      curID: this.$store.state.localStorage.user.id,
      db: this.$fire.firestore,
      timers: {
        hour: 0,
        minute: 0,
        second: 0,
      },
      hour: 0,
      minute: 0,
      second: 0,
    };
  },
  computed: {
    // show minutes
    now: function () {
      return Date.now().toLocaleString();
    },
    accepted() {
      if (isAccept == 1) {
        return true;
      } else {
        return false;
      }
    },

    // timerMinutes() {
    //   const minutes = Math.floor(this.totalSeconds / 60);
    //   return this.formatTime(minutes);
    // },
    // // show seconds
    // timerSeconds() {
    //   let sec = this.totalSeconds % 60;
    //   return this.formatTime(sec);
    // },
  },
  async created() {
    pre_curID = this.$store.state.localStorage.user.id;
    if (!this.user) this.$route.push("/login");
    this.receiver = await (
      await axios.get(baseURL + "/api/user/" + this.recv_id)
    ).data.result;
    if (this.receiver.expert == 1) {
      this.isExpert = 0;
      this.disabled = 1;
    } else {
      this.isExpert = 1;
      // this.disabled = 0;
    }
    console.log("expert:", this.isExpert);
    this.fetchAccepted();
    this.fetchMessages();
    console.log("acceptedfsdafdsa: ", this.acceptedstate.accept);

    // this.isAccepted();
  },
  computed: {
    changes: {
      get: function () {
        return this.second;
      },
      set: function (v) {
        this.second = v;
      },
    },
    second1() {
      return this.second;
    },
  },
  methods: {
    // formats time function
    formatTime(time) {
      if (time < 10) {
        return "0" + time;
      }
      console.log("time", time);
      return time.toString();
    },
    hide() {
      this.is_shown = false;
    },

    show() {
      this.is_shown = true;
    },
    //  check if the expert should do click accept button...
    isAccepted() {},
    // When you click one button among accpet and decline buttons...
    hideADButtons() {
      this.is_shown_buttons = false;
      this.isCustomsAccepted = true;
      console.log("activeB: ", this.isAccept);
      this.disabled = 0;
      let acceptinfo = {
        id: Date.now(),
        accept: "accept",
        expertId: this.$store.state.localStorage.user.id,
        chat: "no",
      };
      this.db.collection("accepted").add(acceptinfo);
    },

    hideDAButtons() {
      this.is_shown_buttons = false;
      this.disabled = 1;
      let acceptinfo = {
        id: Date.now(),
        accept: "decline",
        expertId: this.$store.state.localStorage.user.id,
        chat: "no",
      };
      this.db.collection("accepted").add(acceptinfo);
    },
    //send message function from A to B...
    sendMsg() {
      if (!this.curMsg.trim()) return;
      let msg;
      if (this.isCustomsAccepted == true) {
        msg = {
          id: Date.now(),
          message: this.curMsg,
          userid: this.user.id,
          type: null,
          isCustomAccepted: true,
        };
      } else {
        msg = {
          id: Date.now(),
          message: this.curMsg,
          userid: this.user.id,
          type: null,
          isCustomAccepted: false,
        };
      }
      this.db
        .collection("chat")
        .add(msg)
        .then(function (docRef) {
          this.curMsg = "";
        })
        .catch(function (error) {
          console.error("Error adding document: ", error);
        });
      this.curMsg = "";
      let nDif = 0;
      let detectAccept = 0;
      let nMsg = this.messages.length;
      this.messages.forEach(function (item) {
        if (item.isCustomAccepted !== false) {
          detectAccept++;
        }
      });
      if (detectAccept == 0) {
        this.isAccept = 0; // when the user sends one message without accepting from expert
        this.is_shown_buttons = false;
        this.isCustomsAccepted = false;
        this.firstshow = true;
      } else {
        this.isAccept = 1;
        this.is_shown_buttons = true;
        this.isCustomsAccepted = false;
      }
      if (this.acceptedstate.accept == null) {
        let acceptinfo = {
          id: Date.now(),
          accept: "unaccept",
          expertId: this.$store.state.localStorage.user.id,
          chat: "no",
        };
        this.db.collection("accepted").add(acceptinfo);
      }
    },
    // fetch accepted when loads web pages...
    async fetchAccepted() {
      const docRef = await this.db.collection("accepted");
      docRef.orderBy("id").onSnapshot((querySnapshot) => {
        const allowchat = querySnapshot.isEmpty
          ? null
          : querySnapshot.docs[querySnapshot.docs.length - 1];
        if (allowchat == null) {
          this.acceptedstate = {
            id: Date.now(),
            accept: null,
            expertId: this.$store.state.localStorage.user.id,
            chat: "no",
          };
        } else {
          this.acceptedstate = allowchat.data();
          this.disabled = 0;
          console.log(
            "hahahad",
            this.acceptedstate.accept,
            this.acceptedstate.id
          );
        }
      });
    },
    // fetch messages when loads web pages...
    async fetchMessages() {
      const docRef = await this.db.collection("chat");
      docRef.orderBy("id").onSnapshot(
        (querySnapshot) => {
          if (querySnapshot.empty) {
            console.log("No matching documents.");
            // return;
          }
          const allMessages = [];
          querySnapshot.forEach((doc) => {
            if (doc.exists) {
              allMessages.push(doc.data());
            } else {
              console.log("nothing");
            }
          });
          console.log("I am very happy on this", pre_curID, allMessages);
          this.messages = allMessages;
          this.arr = false;
          let nDif = 0;
          let detectAccept = 0;
          let nMsg = this.messages.length;
          this.messages.forEach(function (item) {
            if (item.isCustomAccepted != false) {
              detectAccept++;
            }
          });
          if (detectAccept == 0) {
            this.isAccept = 0; // when the user sends one message without accepting from expert
            this.is_shown_buttons = true;
            this.isCustomsAccepted = false;
            if (this.isExpert == 1 && this.messages.length != 0) {
              this.firstshow = true;
            }
          } else {
            this.isAccept = 1;
            this.is_shown_buttons = false;
            this.isCustomsAccepted = true;
          }
          console.log(
            "accepted: ",
            this.isAccept,
            nDif,
            pre_curID,
            this.is_shown_buttons,
            this.isCustomsAccepted
          );
        },
        (err) => {
          console.log("error: ${err}");
        }
      );
    },
    // run timer when you click Begin Live Chat Button...
    startChatTimer() {
      const seconds = 0;
      this.timers = {
        hour: "00",
        minute: "00",
        second: "00",
      };
      var timer = setInterval(this.incrementTime, 1000);
      let acceptinfo = {
        id: Date.now(),
        accept: "accept",
        expertId: this.$store.state.localStorage.user.id,
        chat: "yes",
      };
      this.db.collection("accepted").add(acceptinfo);
      this.isActive = true;
      //this.hasChatStarted = true;
    },
    endChatTimer() {
      clearInterval(this.pomodoroInstance);
      this.isActive = false;
    },
    incrementTime() {
      this.totalSeconds++;
      this.timers.hour = Math.floor(this.totalSeconds / 3600);
      this.timers.minute = Math.floor(
        (this.totalSeconds - this.timers.hour * 3600) / 60
      );
      this.timers.second =
        this.totalSeconds - (this.timers.hour * 3600 + this.timers.minute * 60);

      if (this.timers.hour < 10) this.timers.hour = "0" + this.timers.hour;
      if (this.timers.minute < 10)
        this.timers.minute = "0" + this.timers.minute;
      if (this.timers.second < 10)
        this.timers.second = "0" + this.timers.second;
      this.hour = this.timers.hour;
      this.minute = this.timers.minute;
      this.second = this.timers.second;
    },
  },
};
</script>

<style>
.hide_sidebar {
  display: none;
}
.hide_buttons {
  display: none;
}
.show-end-chat-button {
  display: block;
}
.hide-end-chat-button {
  display: none;
}
.started-chat {
  display: none;
}
.large_side {
  grid-column-start: 2;
  grid-column-end: 6;
}
.show {
  visibility: visible;
}
.show_side {
  grid-column-start: 1;
  grid-column-end: 2;
  visibility: visible;
  margin-top: 150px;
  margin-left: 10px;
}
</style>
