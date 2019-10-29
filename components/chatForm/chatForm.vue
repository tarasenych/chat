<template lang="pug">
  form.chatForm(@submit="onSubmit")
    textarea.chatForm__area(
      :value="messageText",
      @input="updateValue",
      @keyup.enter="onSubmit",
      placeholder="Введите что-нибудь и нажмите Enter"
    )
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
    padding: 20px;
    height: 150px;
    width: 100%;

    &__area {
      background-color: #fff;
      border: 1px solid #d3d9de;
      border-radius: 10px;
      resize: none;
      padding: 10px;
      height: 100%;
      width: 100%;
    }
  }
</style>
