
<template>
    <div class="w-25 chat-sidebar border-right">
      <ul class="list-group">
        <li 
          v-for="chat in chats" 
          :key="chat.id" 
          class="list-group-item list-group-item-action"
          @click="$emit('select-chat', chat)"
        >
          <div class="d-flex align-items-center" style="cursor: pointer;">
            <img :src="chat.avatar" alt="Avatar" class="rounded-circle me-2"  style="width: 40px; height: 40px; cursor: pointer;">
            <div class="flex-grow-1 d-flex justify-content-between">
              <div class="name-time-container">
                <strong style="cursor: pointer;" class="chat-name">{{ chat.name }}</strong>
                <small style="cursor: pointer;" class="chat-time">{{ chat.lastMessageTime }}</small>
              </div>
            </div>
          </div>
          <p style="cursor: pointer;" class="mb-0 text-muted">{{ chat.lastMessage }}</p>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['chats']
  };
  </script>
  
  <style scoped>
  .chat-sidebar {
    background-color: #f8f9fa;
  }
  
  .name-time-container {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }
  
  .chat-name {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  
  .chat-time {
    font-size: 0.8rem; /* Adjust font size for the timestamp */
  }
  
  .list-group-item {
    display: flex;
    flex-direction: column;
  }
  </style> 
  


























<!-- <template>
    <div class="w-25 chat-sidebar border-right">
      <ul class="list-group">
        <li 
          v-for="chat in chats" 
          :key="chat.id" 
          class="list-group-item list-group-item-action"
          @click="$emit('select-chat', chat)"
        >
          <div class="d-flex justify-content-between">
            <img :src="chat.avatar" alt="Avatar" class="rounded-circle me-2" style="width: 40px; height: 40px;">
            <strong>{{ chat.name }}</strong>
            <small>{{ chat.lastMessageTime }}</small>
          </div>
          <p class="mb-0 text-muted">{{ chat.lastMessage }}</p>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['chats']
  };
  </script>
  
  <style scoped>
  .chat-sidebar {
    background-color: #f8f9fa;
  }
  </style>
   -->