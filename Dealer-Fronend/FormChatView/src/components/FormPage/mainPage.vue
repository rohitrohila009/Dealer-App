<template>
<div>
   <h5>Chat</h5> 
    <div class="row">
        <Leftside v-on:UserDetails="UserDetails($event)"
        v-bind:arrayOfUsers="ListDetails"
        />
        <MiddlePart v-bind:userChatData="userData" />
          <beautiful-chat
            :participants="participants"
            :titleImageUrl="titleImageUrl"
            :onMessageWasSent="onMessageWasSent"
            :messageList="messageList"
            :newMessagesCount="newMessagesCount"
            :isOpen="isChatOpen"
            :close="closeChat"
            :open="openChat"
            :showEmoji="false"
            :showFile="true"
            :showEdition="true"
            :showDeletion="true"
            :showTypingIndicator="showTypingIndicator"
            :showLauncher="false"
            :showCloseButton="true"
            :colors="colors"
            :alwaysScrollToBottom="alwaysScrollToBottom"
            :disableUserListToggle="false"
            :messageStyling="messageStyling"
            @onType="handleOnType"
            @edit="editMessage"
            />
    </div>
</div>    
</template>
<script>
import Leftside from './leftside'
import MiddlePart from './middlePart'
export default {
    name:'mainPage',
    components:{
        Leftside,
        MiddlePart
    },
    data(){
        return{
            userData:'',
             text12: "",         
       participants: [
        {
          id: "user1",
          name: "Avinash",
          imageUrl:
            "https://avatars3.githubusercontent.com/u/1915989?s=230&v=4",
        },
      ],
      titleImageUrl:
        "https://a.slack-edge.com/66f9/img/avatars-teams/ava_0001-34.png",
      messageList: [],
      newMessagesCount: 0,
      isChatOpen: false,
      showTypingIndicator: "",
      colors: {
        header: {
          bg: "#4e8cff",
          text: "#ffffff",
        },
        launcher: {
          bg: "#4e8cff",
        },
        messageList: {
          bg: "#ffffff",
        },
        sentMessage: {
          bg: "#4e8cff",
          text: "#ffffff",
        },
        receivedMessage: {
          bg: "#eaeaea",
          text: "#222222",
        },
        userInput: {
          bg: "#f4f7f9",
          text: "#565867",
        },
      },
      alwaysScrollToBottom: false,
      messageStyling: true,
      client: "",
      con: "",
      noDealear: false,
      allFriendlyName: [],
      BodyOfMessages: [],
      authors: [],
      allDetails: [],

      ListDetails: [],
      msgDetails: [],
    };
  },
  created() {
    this.openChat();
  },
  methods: {
    UserDetails(e){
            this.userData=e
            console.log(e)
    },
    sendMessage(text) {
      if (text.length > 0) {
        this.newMessagesCount = this.isChatOpen
          ? this.newMessagesCount
          : this.newMessagesCount + 1;
        this.onMessageWasSent({
          author: "support",
          type: "text",
          data: { text },
        });
      }
    },
    dealerNotFound() {
      if (this.noDealear === false) {
        let messageReceived = {
          author: "user2",
          type: "text",
          data: { text: "Dealer is not available" },
        };
        this.messageList.push(messageReceived);
        this.messageList.push({
          author: "user2",
          type: "text",
          data: {
            text:
              "Please share your Name, Contact Numer and Email. So that Dealar can contact you soon.",
          },
        });
      }
    },
    async onMessageWasSent(message) {
      this.con.sendMessage(message.data.text);
      //setTimeout(() => this.delerNotFound(), 5000  );
      this.messageList = [...this.messageList, message];
    },
    callOn(xyz) {
      if (xyz.author !== "rohit") {
        console.log(xyz.state);
        let msgRecived = xyz.state.body;
        let messageReceived = {
          author: "user1",
          type: "text",
          data: { text: msgRecived },
        };
        this.messageList.push(messageReceived);
        this.noDealear = true;
      }
      // if (xyz.author=="rohit"){
      //   setTimeout(() => this.dealerNotFound(), 10000  );
      // }
    },
    async openChat() {
      this.isChatOpen = true;
      // this.newMessagesCount = 0;
      // this.client = await Twilio.Conversations.Client.create("eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCIsImN0eSI6InR3aWxpby1mcGE7dj0xIn0.eyJqdGkiOiJTSzMwYjExYzlhZWUyZjg3OTE5MjI4ODYwMzZmOTM3ZDA4LTE2MTU2MzY5OTciLCJncmFudHMiOnsiaWRlbnRpdHkiOiJyb2hpdCIsInZpZGVvIjp7fSwiY2hhdCI6eyJzZXJ2aWNlX3NpZCI6IklTYjJiODM1YmUzYzI5NDdkNTlkZmU3NmRmYjkwZDIzYzcifSwiZGF0YV9zeW5jIjp7InNlcnZpY2Vfc2lkIjoiZGVmYXVsdCJ9fSwiaWF0IjoxNjE1NjM2OTk3LCJleHAiOjE2MTU3MjMzOTcsImlzcyI6IlNLMzBiMTFjOWFlZTJmODc5MTkyMjg4NjAzNmY5MzdkMDgiLCJzdWIiOiJBQzM3NWFjZjVkNjUzYzNkOWIzMmE4ZDA2MzllY2Y0NjVmIn0.MbyfYgKMqfq1I8EGVGRbdUuVPvTfgpm7XVDrF1HHA-4"
      // );
      // let listOfCOnversation = await this.client.getSubscribedConversations();
      // // let obj = {frndlyName:"",date:"",author:"",itemsmsg:"", sId:"",uID:""}
      // let obj;
      // let obj2;
      // for (var i = 0; i < listOfCOnversation.items.length; i++) {
      //   // console.log(
      //   //   listOfCOnversation.items[i].friendlyName +
      //   //     " ," +
      //   //     listOfCOnversation.items[i].dateUpdated
      //   // );
      //   obj = {
      //     frndlyName: listOfCOnversation.items[i].friendlyName,
      //     date: listOfCOnversation.items[i].dateUpdated,
      //     msgDetails: [],
      //   };
      //   this.ListDetails.push(obj);
      //   let listOfMessages = await listOfCOnversation.items[i].getMessages();
      //   for (var j = 0; j < listOfMessages.items.length; j++) {
      //     obj2 = {
      //       author: listOfMessages.items[j].author,
      //       itemsmsg: listOfMessages.items[j].body,
      //       sId: listOfMessages.items[j].sid,
      //       uID: listOfMessages.items[j].uniqueName,
      //     };
      //     this.ListDetails[i].msgDetails.push(obj2);

      //     // this.msgDetails.push(obj2);
      //     // console.log(
      //     //   listOfMessages.items[j].author + " ," + listOfMessages.items[j].body
      //     // );
      //   }
      // }
      // // console.log(listOfCOnversation.items);
      // // console.log(this.client);

      // // console.log(this.client.user);

      // // console.log(this.client.user.identity);
      // console.log(this.ListDetails);
      // console.log(this.msgDetails);

      // this.$emit("leftDataFetch", { chatDeatils: this.ListDetails });
      // this.con.on("messageAdded", (xyz) => this.callOn(xyz));
    },
    async closeChat() {
      this.isChatOpen = false;
      await this.con.leave();
      await this.client.shutdown();
      console.log(this.client);
    },
    handleScrollToTop() {
      // called when the user scrolls message list to top
      // leverage pagination for loading another page of messages
    },
    handleOnType() {
      console.log("Emit typing event");
    },
    editMessage(message) {
      const m = this.messageList.find((m) => m.id === message.id);
      m.isEdited = true;
      m.data.text = message.data.text;
    },
}
    
}
</script>