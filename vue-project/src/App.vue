
 <template>
  <div id="appvue" class="d-flex shadow m-2 container-fluid">
    <!-- Sidebar for chat persons -->
    <ChatSidebar :chats="chats" @select-chat="selectChat" />

    <!-- Main chat window -->
    <ChatWindow  :activeChat="activeChat" @send-message="sendMessage" />
    <!-- <ChatWindow :activeChat="currentChat" @send-message="handleSendMessage"/> -->
  </div>
</template>

<script>
import ChatSidebar from './components/ChatSidebar.vue';
import ChatWindow from './components/ChatWindow.vue';

export default {
  components: {
    ChatSidebar,
    ChatWindow
  },
  data() {
    return {
      chats: [
        {
          id: 1,
          name: 'John Doe',
          lastMessage: 'Hey, how are you?',
          lastMessageTime: '10:30 AM',
           avatar: 'https://tse1.mm.bing.net/th?id=OIP.X9gYA6VDsnaSpMqBOWKH5wHaGv&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Hello!', sender: 'me' },
            { id: 2, text: 'Hey, how are you?', sender: 'John Doe' },
          ]
        },
        {
          id: 2,
          name: 'Jane Smith',
          lastMessage: 'Are we meeting today?',
          lastMessageTime: 'Yesterday',
           avatar: 'https://tse3.mm.bing.net/th?id=OIP.hvnLMouI3oxrDanXOSmC0wHaHw&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Are we meeting today?', sender: 'Jane Smith' },
            { id: 2, text: 'Yes, let me know the time.', sender: 'me' },
          ]
        },
        {
          id: 3,
          name: 'John sina',
          lastMessage: 'yes it was good ',
          lastMessageTime: 'Yesterday',
           avatar: 'https://tse4.explicit.bing.net/th?id=OIP.E-nFpaLky8KfA1mYdvSsSwHaFj&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Are we meeting today?', sender: 'Jane Smith' },
            { id: 2, text: 'Yes, let me know the time.', sender: 'me' },
          ]
        },
        {
          id: 4,
          name: 'Ben stokes',
          lastMessage: 'Yes, let me know the time. ',
          lastMessageTime: 'Yesterday',
           avatar: 'https://www.vhv.rs/dpng/d/551-5511364_circle-profile-man-hd-png-download.png',
          messages: [
            { id: 1, text: 'we will go home soon', sender: 'Jane Smith' },
            { id: 2, text: 'Yes, let me know the time.', sender: 'me' },
          ]
        },
        {
          id: 5,
          name: 'Amilia co',
          lastMessage: 'Hey wanna meet today',
          lastMessageTime: 'Yesterday',
           avatar: 'https://cdn2.f-cdn.com/files/download/38545966/4bce6b.jpg',
          messages: [
            { id: 1, text: 'Hey wanna meet today', sender: 'Jane Smith' },
            { id: 2, text: 'ket me know the time ', sender: 'me' },
          ]
        },
        {
          id: 6,
          name: 'Alister cook',
          lastMessage: 'Hey, how are you?',
          lastMessageTime: '10:30 AM',
           avatar: 'https://tse1.mm.bing.net/th?id=OIP.X9gYA6VDsnaSpMqBOWKH5wHaGv&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Hello!', sender: 'me' },
            { id: 2, text: 'Hey, how are you?', sender: 'John Doe' },
          ]
        },
        {
          id: 7,
          name: 'Stiven Smith',
          lastMessage: 'Are we meeting today?',
          lastMessageTime: 'Yesterday',
           avatar: 'https://tse3.mm.bing.net/th?id=OIP.hvnLMouI3oxrDanXOSmC0wHaHw&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Are we meeting today?', sender: 'Jane Smith' },
            { id: 2, text: 'Yes, let me know the time.', sender: 'me' },
          ]
        },
        {
          id: 8,
          name: 'Shaun tate',
          lastMessage: 'yes it was good ',
          lastMessageTime: 'Yesterday',
           avatar: 'https://tse4.explicit.bing.net/th?id=OIP.E-nFpaLky8KfA1mYdvSsSwHaFj&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Are we meeting today?', sender: 'Jane Smith' },
            { id: 2, text: 'Yes, let me know the time.', sender: 'me' },
          ]
        },
        {
          id: 9,
          name: 'Michel jhonson',
          lastMessage: 'yes it was good ',
          lastMessageTime: 'Yesterday',
           avatar: 'https://tse4.explicit.bing.net/th?id=OIP.E-nFpaLky8KfA1mYdvSsSwHaFj&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Are we meeting today?', sender: 'Jane Smith' },
            { id: 2, text: 'Yes, let me know the time.', sender: 'me' },
          ]
        }
      ],
      activeChat: {}
    };
  },
  mounted() {
    this.activeChat = this.chats[0]; // Set the first chat as active by default
  },
  methods: {
    selectChat(chat) {
      this.activeChat = chat;
    },
    sendMessage(message) {
      this.activeChat.messages.push({
        id: this.activeChat.messages.length + 1,
        text: message,
        sender: 'me'
      });
    },
  }
};
</script>

<style>
#app {
  display: flex;
  /* background-color: #E4E4E4; */
  padding: 0%;
  margin: 0%;
  width: 100%;
  height: max-content;
}



 #appvue {
  width: 100%;
  /* @media (min-width: 1400px) { 
    width: 100%;
   } */

} 
</style>










<!-- <template>
  <div class="container">
    <ChatComponent />
  </div>
</template>

<script>
import ChatComponent from './components/ChatComponent.vue';

export default {
  name: 'App',
  components: {
    ChatComponent,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style> --> 
