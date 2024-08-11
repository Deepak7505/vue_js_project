 <template>
    <div class="container chat-window flex-grow-1 d-flex flex-column">
      <div class="chat-header p-3 border-bottom">
        <img :src="activeChat.avatar" alt="Avatar" class="rounded-circle me-2" style="width: 40px; height: 40px;">
        <strong>{{ activeChat.name }}</strong>
      </div>
      <div class="chat-messages flex-grow-1 p-3">
        <div :style="{ textAlign: message.text.text ? 'right' : 'left' }"
          v-for="message in activeChat.messages" 
          :key="message.id" 
          :class="['message', message.text.text ? 'text-right' : 'text-left']"
        >
          <div class="p-2 my-2 rounded bg-light d-inline-block">
            {{ message.text.text ? message.text.text : message.text }}
              {{ console.log(message,'this is in the box ') }}
          </div>
        </div>

        
      </div>
      <div class="chat-input p-3 border-top">
        <div class="w-100 d-flex chatcomponent">
          <input 
            type="text" 
            class="form-control" 
            placeholder="Type a message" 
            v-model="newMessage"
            @keyup.enter="sendMessage"
          />
          <img :src="sendicon" alt="Send Icon" class="rounded-circle me-2" style="width: 40px; height: 40px;" @click="sendMessage"/>
        </div>
      </div>
    </div>
  </template>


<script>
export default {
  props: ['activeChat'],
  data() {
    return {
      newMessage: '',
      sendicon: 'https://tse4.mm.bing.net/th?id=OIP.DmuM5OcMrkc08lmO4Ht2EgHaHa&pid=Api&P=0&h=180'
    };
  },
  methods: {
    sendMessage() {
      if (this.newMessage.trim() === '') return;

      // Emit the message with the necessary data
      this.$emit('send-message', {
        text: this.newMessage,
        sender: 'me'
      });

      // Clear the input field
      this.newMessage = '';
    }
  }
}
</script>



<style scoped>
.chat-window {
  background-color: #fff;
}

.message.text-right .bg-light {
  background-color: #dcf8c6;
}

.chat-input {
  background-color: #fff;
  border-radius: 1rem;
  margin-bottom: 1rem;
}
</style>


























<!-- <template>
    <div class="container  chat-window flex-grow-1 d-flex flex-column">
      <div class="chat-header p-3 border-bottom">
        <img :src="activeChat.avatar" alt="Avatar" class="rounded-circle me-2" style="width: 40px; height: 40px;">
        <strong>{{ activeChat.name }}</strong>
      </div>
      <div class="chat-messages flex-grow-1 p-3">
        <div 
          v-for="message in activeChat.messages" 
          :key="message.id" 
          :class="['message', message.sender === 'me' ? 'text-right' : 'text-left']"
        >
          <div class="p-2 my-2 rounded bg-light d-inline-block">
            {{ message.text }}
          </div>
        </div>
      </div>
      <div class="chat-input p-3 border-top ">
        <div class="w-100 d-flex chatcomponent " >
                <input 
            type="text" 
            class="form-control" 
            placeholder="Type a message" 
            v-model="newMessage"
            @keyup.enter="sendMessage"
            
            />
            <img :src="sendicon" alt="Avatar" class="rounded-circle me-2" style="width: 40px; height: 40px;">
        </div>

      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['activeChat'],
    data() {
      return {
        newMessage: '',
        sendicon: 'https://tse4.mm.bing.net/th?id=OIP.DmuM5OcMrkc08lmO4Ht2EgHaHa&pid=Api&P=0&h=180'
      };
    },
    methods: {
      sendMessage() {
        if (this.newMessage.trim() === '') return;
  
        this.$emit('send-message', this.newMessage);
        this.newMessage = '';
      }
    }
  };
  </script>
  
  <style scoped>
  .chat-window {
    background-color: #fff;
  }
  
  .message.text-right .bg-light {
    background-color: #dcf8c6;
  }
  
  .chat-input {
    background-color: #fff;
    border-radius: 1rem;
    margin-bottom: 1rem;
  }
  </style>
   -->