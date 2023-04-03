<template>
  <div class="chatbot">
    <div class="messages" ref="messages">
      <div v-for="(message, index) in messages" :key="index">
        <div v-if="message.isBot" class="bot-message">{{ message.text }}</div>
        <div v-else class="user-message">{{ message.text }}</div>
      </div>
    </div>
    <div class="input">
      <input v-model="currentMessage" @keyup.enter="sendMessage" placeholder="Type a message...">
      <button @click="sendMessage">Send</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      messages: [],
      currentMessage: ''
    }
  },
  methods: {
    sendMessage() {
      if (this.currentMessage) {
        this.messages.push({
          text: this.currentMessage,
          isBot: false
        });
        
        this.fakeBotResponse()
        this.currentMessage = '';
        this.$nextTick(() => {
          this.$refs.messages.scrollTop = this.$refs.messages.scrollHeight;
        });
      }
    },
    fakeBotResponse() {
      if (this.currentMessage) {
        this.messages.push({
          text: "Bot response",
          isBot: true
        });

        this.currentMessage = '';
        this.$nextTick(() => {
          this.$refs.messages.scrollTop = this.$refs.messages.scrollHeight;
        });
      }
    }
  }
}
</script>

<style scoped>
.chatbot {
  display: flex;
  flex-direction: column;
  max-height: 260px
}
.messages {
  flex: 1;
  height: 300px;
  overflow-y: auto;
  padding: 16px;
}


.bot-message {
  background-color: #87CEFA;
  color: #000000;
  padding: 8px;
  border-radius: 8px;
  margin-bottom: 8px;
}


.user-message {
  background-color: #F5F5F5;
  color: #000000;
  padding: 8px;
  border-radius: 8px;
  margin-bottom: 8px;
}

.input {
  display: flex;
  position: fixed;
  bottom: 10px;
  width: 90%;
  padding: 16px;
  background-color: #fff;
  border-top: 1px solid #eee;
  border-radius: 15px;
}

.input input {
  flex: 1;
  margin-right: 16px;
  padding: 8px;
  border-radius: 8px;
  border: none;
}

.input button {
  padding: 8px;
  border-radius: 8px;
  border: none;
  background-color: #87CEFA;
  color: #fff;
  cursor: pointer;
}
.input button:hover {
background-color: #1E90FF;
}

</style>
