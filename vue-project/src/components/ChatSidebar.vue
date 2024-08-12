<template>
  <div class="chat-sidebar border-right-4 shadow">
    <!-- Search Bar -->
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

    <!-- Chat List -->
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
  props: ['chats'],
  data() {
    return {
      searchQuery: "",
    };
  },
  computed: {
    filteredChats() {
      if (!this.searchQuery) {
        return this.chats;
      }
      return this.chats.filter(chat =>
        chat.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    handleSubmit() {
      console.log("Search query:", this.searchQuery);
      // Additional search logic can be implemented here
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

.chat-list {
  overflow-y: auto;
  flex-grow: 1;
}

.name-time-container {
  /* display: flex;
  flex-direction: column;
  align-items: flex-start; */
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: space-evenly;
    width: 100%;
}

.chat-name {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  width:100%;
}

.chat-time {
  font-size: 0.8rem;
  cursor: pointer;
    display: flex;
    width: 100%;
    justify-content: end;
}

.list-group-item {
  display: flex;
  flex-direction: column;
}
</style>



<!-- <template>
  <div class="chat-sidebar border-right-4 shadow container">
    Search Bar
    <div class="row justify-content-center mb-3">
      <div class="col-12">
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
    </div>

    <ul class="list-group row">
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
  props: ['chats'],
  data() {
    return {
      searchQuery: "",
    };
  },
  computed: {
    filteredChats() {
      if (!this.searchQuery) {
        return this.chats;
      }
      return this.chats.filter(chat =>
        chat.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    handleSubmit() {
      console.log("Search query:", this.searchQuery);
      // Additional search logic can be implemented here
    },
  },
};
</script>

<style scoped>
.chat-sidebar {
  background-color: #f8f9fa;
  width: 40%;
  overflow-y: scroll;
  padding-top: 15px;
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
  font-size: 0.8rem;
}

.list-group-item {
  display: flex;
  flex-direction: column;
}
</style>

 -->
