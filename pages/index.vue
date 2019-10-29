<template lang="pug">
  .theChat
    ChatList
      template(v-if="messageList.length > 0")
        ChatMessage(
          v-for="message in messageList",
          :key="message.id",
          :author="message.author",
          :text="message.text",
        ) {{ message.text }}
      p(v-else) На данный момент сообщений нет. Напишите что-нибудь в чат.

    ChatForm(
      :onSubmit="sendMessage",
      v-model="messageText"
    )
</template>

<script>
import ChatForm from '../components/ChatForm/ChatForm';
import ChatList from '../components/ChatList/ChatList';
import ChatMessage from '../components/chatMessage/chatMessage';

export default {
  components: {
    ChatForm,
    ChatList,
    ChatMessage,
  },
  data() {
    return {
      messageList: [],
      messageText: '',
      isLoad: false,
    }
  },
  methods: {
    async sendMessage() {
      event.preventDefault();
      const { messageText } = this;

      if (this.isLoad === true || /^\s{0,}$/.test(messageText)) return;
      this.isLoad = true;

      try {
        const response = await this.$axios.$post('/message', { text: messageText });

        if (response.success !== true) {
          throw(new Error('Server error, please try again'));
        }

        this.messageList.push(
          { author: 'me', text: messageText },
          { author: 'server', text: response.text },
        );

        localStorage.setItem('chatHistory', JSON.stringify(this.messageList));
        this.messageText = '';
      } catch(error) {
        this.messageList.push({ author: 'system', text: error.toString() });
      } finally {
        this.isLoad = false;
      }
    },
  },
  mounted() {
    const messagesHistory = localStorage.getItem('chatHistory');

    if (messagesHistory) {
      this.messageList = JSON.parse(messagesHistory);
    }
  }
}
</script>

<style lang="scss">
  .theChat {
    display: flex;
    flex-direction: column;
    margin: 0 auto;
    height: 100vh;
    width: 90%;
  }
</style>
