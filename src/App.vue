<template>
  <div id="app" class="chat-app">
    <div class="chat-widget">
        <div v-for="message in messages" :key="message.id" class="message" :class="{ 'user': message.isUser, 'bot': !message.isUser }">
          <div v-if="message.isTyping" class="typing-dots"></div>
          <div v-if="!message.isUser" class="avatar-container left">
            <img class="avatar" src="./assets/bot.png" alt="Bot Avatar" />
          </div>
          <div v-if="message.isUser" class="avatar-container right">
            <img class="avatar" src="./assets/user.png" alt="User Avatar" />
          </div>
          {{ message.text }}
          
        </div>
        <div class="options">
      <button v-for="option in options" :key="option" @click="sendMessage(option)" class="button">
        {{ option }}
      </button>
    </div>
    </div>
    
  </div>
</template>

<script>
export default {
  data() {
    return {
      messages: [
        { id: 1, text: "Привет! Что я могу для Вас сделать?", isUser: false },
      ],
      options: ["Заказать пиццу", "Установить будильник", "Вывести погоду"],
    };
  },
  methods: {
    sendMessage(option) {
      this.showTyping(true);
      
      setTimeout(() => {
        this.showTyping(false);
        this.messages.push({ id: this.messages.length + 1, text: option, isUser: true });
        this.showTyping(true);


        setTimeout(() => {
          this.showTyping(false);
          this.messages.push({ id: this.messages.length + 1, text: "Хорошо, я могу " + option.toLowerCase() + ". Что еще могу сделать?", isUser: false });
        }, 2000); // Задержка для ответа бота
      }, 1000); // Задержка для эффекта печати
    },
    showTyping(isTyping) {
      if (isTyping) {
        const typingIndex = this.messages.findIndex((msg) => msg.isTyping);
        if (typingIndex === -1) {
          this.messages.push({ id: this.messages.length + 1, text: '...', isUser: !this.messages[this.messages.length - 1]?.isUser, isTyping });
        }
      } else {
        const typingIndex = this.messages.findIndex((msg) => msg.isTyping);
        if (typingIndex !== -1) {
          this.messages.splice(typingIndex, 1);
        }
      }
    },
  },
};
</script>

<style>
#app {
  height: 100%;
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: flex-end;
}

.chat-app {
  height: 100%;
  width: 300px; 
  margin-right: 20px;
  margin:  0 auto;
}

.chat-widget {
  min-height: 200px;
  flex: 1;
  display: flex;
  flex-direction: column;
  padding: 10px;
  margin-bottom: 10px;
  overflow-y: auto;
  border: 1px solid #ccc;
  border-radius: 10px;

}

.avatar {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  overflow: hidden;
  display: inline-block;
}

.avatar-container {
  display: flex;
}

.avatar-container.left {
  margin-right: 8px;
}

.avatar-container.right {
  order: 2;
}

.message {
  max-width: 70%;
  margin: 5px;
  padding: 8px;
  border-radius: 5px;
  position: relative;
  display: flex;
}



.user {
  align-self: flex-end;
  background-color: #d3f1ff;
  gap: 5px;
}

.bot {
  align-self: flex-start;
  background-color: #f5f3f3;
}

.typing-dots {
  display: inline-block;
  overflow: hidden;
  position: absolute;
  width: 0;
  animation: typing 1s steps(3, end) infinite;
}

@keyframes typing {
  from { width: 0; }
  to { width: 100%; }
}

.options {
  display: flex;
  flex-direction: column;
  justify-self: end;
  gap: 10px;
  margin-top: 15px;
}


.button {
  flex: 1;
  box-shadow: 0 5px 15px 0 rgba(11, 99, 246, 1);
  transition: 0.5s;
  font-size: 14px;
  background-color: rgba(11, 99, 246, 1);
  border: none;
  border-radius: 3px;
  color: aliceblue;
  padding: 10px 15px;
}

.button:hover {
  transform: translate(0,-3px);
  box-shadow: 0 20px 40px 0 rgba(11, 99, 246, 1);
  cursor: pointer;
}

@media (max-width: 770px) {
  #app {
    font-size: 14px;
  }
 
}
</style>
