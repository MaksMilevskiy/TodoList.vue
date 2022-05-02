<template>
  <button>
      <slot></slot>
  </button>
</template>

<script>
export default {
    name: "my-button",
}
</script>

<style scoped>
button {
    align-self: flex-end;
    background-color: white;
    color: teal;
    border: 1px solid teal;
    padding: 10px;
    cursor: pointer;
}
</style>