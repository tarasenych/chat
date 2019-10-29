<template lang="pug">
  form.chatForm(@submit="onSubmit")
    textarea.chatForm__area(:value="messageText", @input="updateValue")
    input.chatForm__submit(type="submit")
</template>

<script>
export default {
  model: {
    prop: 'messageText'
  },
  props: {
    messageText: {
      type: String,
      default: '',
    },
    onSubmit: {
      type: Function,
      default: () => {},
    },
  },
  methods: {
    updateValue({ target }) {
      this.$emit('input', target.value);
    },
  },
}
</script>

<style lang="scss">
  .chatForm {
    background-color: #fafbfc;
    flex-shrink: 0;
    height: 200px;
    padding: 20px;

    &__area {
      background-color: #eeeeee;
      border: 1px solid #aaaaaa;
      resize: none;
      height: 100%;
      width: 80%;
    }
  }
</style>
