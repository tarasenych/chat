<template lang="pug">
  .chatList
    slot
</template>

<script>
export default {

}
</script>

<style lang="scss">
  .chatList {
    display: flex;
    flex-grow: 1;
    flex-direction: column;
    overflow-y: auto;
    padding: 20px 10px;
  }
</style>