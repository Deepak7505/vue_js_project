 <template>
  <div class="container chat-window w-100 flex-grow-1 d-flex flex-column">
    <div class="chat-header p-3 border-bottom">
      <img :src="activeChat.avatar" alt="Avatar" class="rounded-circle me-2" style="width: 40px; height: 40px;">
      <strong>{{ activeChat.name }}</strong>
    </div>

    <div class="chat-messages flex-grow-1 p-3">
      <div :style="{ textAlign: message.text.text ? 'right' : 'left' }"
        v-for="message in activeChat.messages" 
        :key="message.id" 
        :class="['message', message.text.text ? 'text-right' : 'text-left '] "
      >
        <div class="p-2 my-2 rounded chat-text d-inline-block">
          {{ message.text.text ? message.text.text : message.text }}
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
        <button class="btn btn-secondary ms-2" @click="openTemplateModal">Template</button>
        <img :src="sendicon" alt="Send Icon" class="rounded-circle me-2" style="width: 40px; height: 40px; cursor: pointer;" @click="sendMessage"/>
      </div>
    </div>

    
    <div v-if="isTemplateModalOpen" class="template-modal">
      <div class="modal-content row p-4">
        <div class="col-12 d-flex align-items-start mb-4">
          <h3 class="me-auto">Select a Template</h3>
          <button class="btn-close ms-auto" @click="closeTemplateModal">X</button>
        </div>

        <div :class="['template-list', { 'col-12': !selectedTemplate, 'col-md-8': selectedTemplate }]" style="position: relative;">
          <div 
            v-for="template in templates" 
            :key="template.id" 
            @click="selectTemplate(template)" 
            :class="['template-item', 'mb-3', 'card', 'p-3', { 'selected': template.id === selectedTemplate?.id }]"
          >
            <h5>{{ template.title }}</h5>
            <p>{{ template.description }}</p>
          </div>


        </div>

          

        <div v-if="selectedTemplate" class="template-customization">
            <h4>Customize Template</h4>
            <div v-for="(field, index) in selectedTemplate.fields" :key="index" class="mb-2">
              <label :for="'field-' + index" class="form-label">{{ field.label }}</label>
              <input 
                type="text" 
                class="form-control" 
                :id="'field-' + index" 
                v-model="field.value"
              />
            </div>
            <button class="btn btn-primary mt-3 w-100" @click="applyTemplate" :disabled="!isTemplateFilled">Apply</button>
          </div> 
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
      sendicon: 'https://tse4.mm.bing.net/th?id=OIP.DmuM5OcMrkc08lmO4Ht2EgHaHa&pid=Api&P=0&h=180',
      isTemplateModalOpen: false,
      templates: [
        {
          id: 1,
          title: 'Template 1',
          description: 'Hi [Name], Your appointment is on [Date].',
          fields: [
            { label: 'Name', value: '' },
            { label: 'Date', value: '' },
          ]
        },
        {
          id: 2,
          title: 'Template 2',
          description: 'Dear [Name], Your order #[OrderNumber] will be delivered by [Date].',
          fields: [
            { label: 'Name', value: '' },
            { label: 'Order Number', value: '' },
            { label: 'Date', value: '' },
          ]
        },
        // Add more templates (total of 6)
        {
          id: 3,
          title: 'Template 3',
          description: 'Hello [Name], your subscription expires on [Date].',
          fields: [
            { label: 'Name', value: '' },
            { label: 'Date', value: '' },
          ]
        },
        {
          id: 4,
          title: 'Template 4',
          description: 'Hi [Name], your meeting is scheduled on [Date] at [Time].',
          fields: [
            { label: 'Name', value: '' },
            { label: 'Date', value: '' },
            { label: 'Time', value: '' },
          ]
        },
        {
          id: 5,
          title: 'Template 5',
          description: 'Dear [Name], your request #[RequestID] has been processed.',
          fields: [
            { label: 'Name', value: '' },
            { label: 'RequestID', value: '' },
          ]
        },
        {
          id: 6,
          title: 'Template 6',
          description: 'Hi [Name], your payment of [Amount] is due on [Date].',
          fields: [
            { label: 'Name', value: '' },
            { label: 'Amount', value: '' },
            { label: 'Date', value: '' },
          ]
        }
      ],
      selectedTemplate: null,
    };
  },
  computed: {
    isTemplateFilled() {
      if (!this.selectedTemplate) return false;
      return this.selectedTemplate.fields.every(field => field.value.trim() !== '');
    }
  },
  methods: {
    openTemplateModal() {
      this.isTemplateModalOpen = true;
    },
    closeTemplateModal() {
      this.isTemplateModalOpen = false;
      this.selectedTemplate = null;
    },
    selectTemplate(template) {
      this.selectedTemplate = JSON.parse(JSON.stringify(template)); // Deep copy to avoid mutation
    },
    applyTemplate() {
      if (!this.selectedTemplate) return;

      let filledMessage = this.selectedTemplate.description;

      this.selectedTemplate.fields.forEach(field => {
        filledMessage = filledMessage.replace(`[${field.label}]`, field.value);
      });

      this.newMessage = filledMessage;
      this.closeTemplateModal();
    },
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

.chat-text {
  background-color: #eff0f679;
}

.template-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999;
}

.modal-content {
  background-color: white;
  width: 80%;
  max-height: 90%;
  overflow-y: auto;
  padding: 20px;
  border-radius: 10px;
  position: relative;
}

.template-list {
  overflow-y: auto;
  max-height: 60vh;
  /* transition: width 0.8s; */
}


.template-customization {
  position: absolute;
  top: 5rem;
  right: 0;
  /* background-color: #f9f9f9; */
  padding: 20px;
  height: max-content;
  overflow-y: auto;
  width: 35%;
}

.template-item {
  cursor: pointer;
}

.template-item.selected {
  background-color: #e0f7fa;
  border: 1px solid #007bff;
}

.template-item:hover {
  background-color: #f0f0f0;
}

.template-customization input.form-control {
  padding: 5px;
  font-size: 0.9rem;
}

.btn-close {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
}

.btn-close:hover {
  color: red;
}

/* @media (max-width: 768px) {
  .modal-content {
    width: 95%;
    padding: 15px;
  }

  .template-list {
    border-right: none;
    border-bottom: 1px solid #ddd;
    margin-bottom: 20px;
    max-height: 40vh;
  }

  .template-customization {
    position: relative;
    width: 100%;
    border-left: none;
    box-shadow: none;
  }
} */
</style> 


