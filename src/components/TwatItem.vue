<template>
  <div class="twat-item">
    <div class="user-profile__twat">
      <div class="twat-item__user">
        @{{ username }}
      </div>
      <div class="twat-item__content">
        {{ twat.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwootItem",
  props: {
    username: {
      type: String,
      required: true
    },
    twat: {
      type: Object,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
.twat-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;

  &:hover {
    transform: scale(1.1, 1.1);
  }

  .twat-item__user {
    font-weight: bold;
  }
}
</style>