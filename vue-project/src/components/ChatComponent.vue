<template>
    <div class="chat-container">
      <div class="chat-list-container">
        <ChatList :chats="chats" :selectedChatId="selectedChat?.id" @chatSelected="selectChat" />
      </div>
      <div class="chat-content-container">
        <ChatContent :selectedChat="selectedChat" />
      </div>
    </div>
  </template>
  
  <script>
  import ChatList from './ChatList.vue';
  import ChatContent from './ChatContent.vue';
  
  export default {
    components: {
      ChatList,
      ChatContent,
    },
    data() {
      return {
        chats: [
          {
            id: 1,
            name: 'John Doe',
            lastMessage: 'Hey there!',
            messages: [
              { id: 1, sender: 'John Doe', text: 'Hey there!' },
              { id: 2, sender: 'You', text: 'Hello!' },
            ],
          },
          {
            id: 2,
            name: 'Jane Smith',
            lastMessage: 'How are you?',
            messages: [
              { id: 1, sender: 'Jane Smith', text: 'How are you?' },
              { id: 2, sender: 'You', text: 'I am fine, thanks!' },
            ],
          },
        ],
        selectedChat: null,
      };
    },
    methods: {
      selectChat(chat) {
        this.selectedChat = chat;
      },
    },
  };
  </script>
  
  <style scoped>
  .chat-container {
    display: flex;
    height: 100vh;
    width: 100%;
  }
  
  .chat-list-container {
    width: 30%;
    min-width: 300px;
    border-right: 1px solid #ddd;
    background-color: #f1f1f1;
  }
  
  .chat-content-container {
    flex-grow: 1;
    background-color: #fff;
  }
  
  @media (max-width: 768px) {
    .chat-container {
      flex-direction: column;
    }
  
    .chat-list-container {
      width: 100%;
      border-right: none;
      border-bottom: 1px solid #ddd;
    }
  
    .chat-content-container {
      width: 100%;
    }
  }
  </style>
  