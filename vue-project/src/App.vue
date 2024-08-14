 <template>
  <div id="appvue" class="d-flex shadow m-2 container-fluid">

    <ChatSidebar :chats="chats" @select-chat="selectChat" />


    <ChatWindow  :activeChat="activeChat" @send-message="sendMessage" />

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
          unreadCount: 0, // Number of unread messages
          isGroup: false, // Indicates it's an individual chat  
          avatar: 'https://tse1.mm.bing.net/th?id=OIP.TSdjZaOzQAo_pkVZWysyUAHaHa&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Hello!', sender: 'me' },
            { id: 2, text: 'Hey, how are you?', sender: 'John Doe' },
          ]
        },
        {
          id: 2,
          name: 'Trevlers',
          lastMessage: 'Are we meeting today?',
          lastMessageTime: 'Yesterday',
          unreadCount: 4, // Number of unread messages
          isGroup: true, // Indicates it's an individual chat
          avatar: 'https://tse1.mm.bing.net/th?id=OIP.Hgl0WEK0vs03QPwIX73ywQHaHa&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Are we meeting today?', sender: 'Jane Smith' },
            { id: 2, text: 'Yes, let me know the time.', sender: 'me' },
            { id: 1, text: 'I want to know the time', sender: 'Jane Smith' },
            { id: 1, text: 'Are we meeting today?', sender: 'Jane Smith' },

          ]
        },
        {
          id: 3,
          name: 'John sina',
          lastMessage: 'yes it was good ',
          lastMessageTime: 'Yesterday',
          unreadCount: 2, // Number of unread messages
          isGroup: false, // Indicates it's an individual chat
          avatar: 'https://tse1.mm.bing.net/th?id=OIP.TSdjZaOzQAo_pkVZWysyUAHaHa&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Are we meeting today?', sender: 'Jane Smith' },
            { id: 2, text: 'Yes, let me know the time.', sender: 'me' },
          ]
        },
        {
          id: 4,
          name: 'Smith Family',
          lastMessage: 'Yes, let me know the time. ',
          lastMessageTime: 'Yesterday',
          unreadCount: 0, // Number of unread messages
          isGroup: true, // Indicates it's an individual chat
          avatar: 'https://tse1.mm.bing.net/th?id=OIP.Hgl0WEK0vs03QPwIX73ywQHaHa&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'we will go home soon', sender: 'Jane Smith' },
            { id: 2, text: 'Yes, let me know the time.', sender: 'me' },
          ]
        },
        {
          id: 5,
          name: 'The creaters',
          lastMessage: 'Emergency',
          lastMessageTime: 'Yesterday',
          unreadCount: 5, // Number of unread messages
          isGroup: true, // Indicates it's an individual chat
          avatar: 'https://tse1.mm.bing.net/th?id=OIP.Hgl0WEK0vs03QPwIX73ywQHaHa&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Hey wanna meet today', sender: 'Jane Smith' },
            { id: 2, text: 'ket me know the time ', sender: 'me' },
            { id: 1, text: 'Its ', sender: 'Jane Smith' },
            { id: 1, text: 'An ', sender: 'Jane Smith' },
            { id: 1, text: 'Emergency', sender: 'Jane Smith' },

          ]
        },
        {
          id: 6,
          name: 'Alister cook',
          lastMessage: 'Hey, how are you?',
          lastMessageTime: '10:30 AM',
          unreadCount: 0, // Number of unread messages
          isGroup: false, // Indicates it's an individual chat  
          avatar: 'https://tse1.mm.bing.net/th?id=OIP.TSdjZaOzQAo_pkVZWysyUAHaHa&pid=Api&P=0&h=180',
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
          unreadCount: 2, // Number of unread messages
          isGroup: false, // Indicates it's an individual chat
          avatar: 'https://tse1.mm.bing.net/th?id=OIP.TSdjZaOzQAo_pkVZWysyUAHaHa&pid=Api&P=0&h=180',
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
          unreadCount: 0, // Number of unread messages
          isGroup: false, // Indicates it's an individual chat',
          avatar: 'https://tse1.mm.bing.net/th?id=OIP.TSdjZaOzQAo_pkVZWysyUAHaHa&pid=Api&P=0&h=180',
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
          unreadCount: 0, // Number of unread messages
          isGroup: false, // Indicates it's an individual chat
          avatar: 'https://tse1.mm.bing.net/th?id=OIP.TSdjZaOzQAo_pkVZWysyUAHaHa&pid=Api&P=0&h=180',
          messages: [
            { id: 1, text: 'Are we meeting today?', sender: 'Jane Smith' },
            { id: 2, text: 'Yes, let me know the time.', sender: 'me' },
          ]
        }
      ],
      activeChat: {}
    };
  }
  ,
  mounted() {
    this.activeChat = this.chats[0]; // Set the first chat as active by default
  },
  methods: {
  selectChat(chat) {
    chat.unreadCount = 0; // Reset unread count when the chat is selected
    this.activeChat = chat; // Set the selected chat as active
  },
  sendMessage(message) {
    if (this.activeChat && this.activeChat.messages) {
      this.activeChat.messages.push({
        id: this.activeChat.messages.length + 1,
        text: message,
        sender: 'me'
      });
      this.activeChat.lastMessage = message;
      this.activeChat.lastMessageTime = new Date().toLocaleTimeString([], {
        hour: '2-digit',
        minute: '2-digit'
      });
    }
  }
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

