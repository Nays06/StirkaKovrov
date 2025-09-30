<template>
    <div class="button">{{ text }}</div>
</template>

<script>
export default {
  props: {
    text: {
      default: "Оставить заявку",
      type: String
    }
  }
}
</script>

<style scoped>
.button {
  background-color: var(--primary-color);
  padding: 18px 50px;
  border-radius: 3px;
  border: 2px solid var(--primary-color);
  font-size: 16px;
  font-weight: 600;
  text-transform: uppercase;
  color: #ffffff;
  transition: 0.5s;
  margin: 0 auto;
  display: inline-block;
  cursor: pointer;
  user-select: none;
}

.button:hover {
  background-color: transparent;
  color: var(--primary-color);
}
</style>