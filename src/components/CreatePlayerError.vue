<template>
  <div class="errors-list">
    <span
      v-for="message in messages"
      :key="message"
    >
      {{ message }}
    </span>
  </div>
</template>

<script>
export default {
  name: "CreatePlayerError",
  props: {
    messages: Array,
  },
};
</script>

<style lang="scss" scoped>
.errors-list {
  display: flex;
  flex-direction: column;
  color: red;
  gap: 5px;
}
</style>
