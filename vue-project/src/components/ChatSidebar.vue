<template>
  <div class="chat-sidebar border-right-4 shadow">
    
    <div class="search-bar-container">
      <form @submit.prevent="handleSubmit">
        <div class="input-group">
          <input
            type="text"
            class="form-control"
            v-model="searchQuery"
            placeholder="Search or start a new chat"
          />
        </div>
      </form>
    </div>


    <div class="filter-buttons">
      <button
        type="button"
        class="btn mx-1"
        :class="{'active-filter': currentFilter === 'all'}"
        @click="setFilter('all')"
      >
        All
      </button>
      <button
        type="button"
        class="btn mx-1"
        :class="{'active-filter': currentFilter === 'unread'}"
        @click="setFilter('unread')"
      >
        Unread
      </button>
      <button
        type="button"
        class="btn mx-1"
        :class="{'active-filter': currentFilter === 'group'}"
        @click="setFilter('group')"
      >
        Group
      </button>
    </div>

    
    <ul class="list-group chat-list">
      <li
        v-for="chat in filteredChats"
        :key="chat.id"
        class="list-group-item list-group-item-action"
        @click="$emit('select-chat', chat)"
      >
        <div class="d-flex align-items-center" style="cursor: pointer;">
          <img
            :src="chat.avatar"
            alt="Avatar"
            class="rounded-circle me-2"
            style="width: 40px; height: 40px; cursor: pointer;"
          />
          <div class="flex-grow-1 d-flex justify-content-between">
            <div class="name-time-container">
              <div>
                <strong style="cursor: pointer;"
                
                class="chat-name" >
                {{ chat.name }}

              </strong>
              <!-- <p style="cursor: pointer;" class="mb-0 text-muted">{{ chat.text ? chat.text ? : chat.lastMessage }}</p> -->
              <p style="cursor: pointer;" class="mb-0 text-muted">{{  chat.lastMessage.text ?  chat.lastMessage.text : chat.lastMessage  }}</p>

              </div>
              <div class="flex">
                <small style="cursor: pointer;" class="chat-time">{{ chat.lastMessageTime }}</small>
                <span v-if="chat.unreadCount > 0" class="badge bg-success ms-2">{{ chat.unreadCount }}</span>
              </div>
            </div>
          </div>
        </div>

      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['chats'],
  data() {
    return {
      searchQuery: "",
      currentFilter: "all",
    };
  },
  computed: {
  filteredChats() {
    let filtered = this.chats;

    if (this.currentFilter === 'unread') {
      filtered = filtered.filter(chat => chat.unreadCount > 0);  // Show chats with unread messages
    } else if (this.currentFilter === 'group') {
      filtered = filtered.filter(chat => chat.isGroup);
    }

    if (this.searchQuery) {
      filtered = filtered.filter(chat =>
        chat.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    }

    return filtered;
  },
}
,
  methods: {
    handleSubmit() {
      console.log("Search query:", this.searchQuery);
      // Additional search logic can be implemented here
    },
    setFilter(filter) {
      this.currentFilter = filter;
    },
  },
};
</script>

<style scoped>
.chat-sidebar {
  background-color: #f8f9fa;
  width: 40%;
  height: 100vh; /* Full viewport height */
  display: flex;
  flex-direction: column;
}

.search-bar-container {
  position: sticky;
  top: 0;
  z-index: 1000;
  background-color: #dbdfe3;
  padding: 15px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.filter-buttons {
  display: flex;
  /* justify-content: space-around; */
  padding: 10px 0;
  background-color: #f8f9fa;
  border-bottom: 1px solid #ddd;
}

.filter-buttons .btn {
  border: none;
  background-color: rgb(233, 230, 230);
  font-weight: bold;
  cursor: pointer;
}

.filter-buttons .btn.active-filter {
  /* color: #007bff; */
  color: rgb(2, 126, 2);
  background-color: rgb(212, 207, 207);
}

.chat-list {
  overflow-y: auto;
  flex-grow: 1;
}

.name-time-container {
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  justify-content: space-between;
  width: 100%;
}

.chat-name {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    width: 100%;
    position: relative;
    top: 0.2rem;
}

.chat-time {
  font-size: 0.8rem;
  display: flex;
  width: max-content;
  justify-content: end;
}

.list-group-item {
  display: flex;
  flex-direction: column;
}
</style>






<!-- <ul class="list-group chat-list">
  <li
    v-for="chat in filteredChats"
    :key="chat.id"
    class="list-group-item list-group-item-action"
    @click="$emit('select-chat', chat)"
  >
    <div class="d-flex align-items-center" style="cursor: pointer;">
      <img
        :src="chat.avatar"
        alt="Avatar"
        class="rounded-circle me-2"
        style="width: 40px; height: 40px; cursor: pointer;"
      />
      <div class="flex-grow-1 d-flex justify-content-between">
        <div class="name-time-container">
          <div style="display: contents;">
            <strong style="cursor: pointer;"
            :style="{
              top: chat.unreadCount > 0 ? '0.5rem' : '0rem'
            }"
            class="chat-name" >
            {{ chat.name }}

          </strong>
          </div>
          <div class="flex">
            <small style="cursor: pointer;" class="chat-time">{{ chat.lastMessageTime }}</small>
            <span v-if="chat.unreadCount > 0" class="badge bg-success ms-2">{{ chat.unreadCount }}</span>
          </div>
        </div>
      </div>
    </div>
    <p style="cursor: pointer;" class="mb-0 text-muted">{{ chat.lastMessage }}</p>
  </li>
</ul> -->