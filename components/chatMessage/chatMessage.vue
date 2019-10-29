<template lang="pug">
  .chatMessage(:class="messageClasses") {{ text }}
</template>

<script>
  export default {
  props: {
    author: {
      type: String,
      default: '',
    },
    text: String,
  },
  computed: {
    messageClasses() {
      return {
        'chatMessage--right': this.author === 'server',
        'chatMessage--system': this.author === 'system',
      };
    },
  },
  mounted() {
    this.$el.scrollIntoView(false);
  }
}
</script>

<style lang="scss">
  .chatMessage {
    align-self: flex-start;
    background-color: #4962D6;
    border-radius: 5px;
    color: #ffffff;
    max-width: 40%;
    padding: 10px;

    & + & {
      margin-top: 10px;
    }

    &--right {
      align-self: flex-end;
      background-color: #6F81D6;
    }

    &--system {
      background-color: #FFB400;
      color: #000;
      max-width: none;
      width: 100%;
    }
  }
</style>