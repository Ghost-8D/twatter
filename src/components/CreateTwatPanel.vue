<template>
  <form class="create-twat-panel" @submit.prevent="createNewTwat" :class="{ '--exceeded': newTwatCharacterCount > 180 }">
    <label for="newTwat"><strong>New Twat</strong> ({{ newTwatCharacterCount }}/180)</label>
    <textarea id="newTwat" rows="4" v-model="state.newTwatContent"/>

    <div class="create-twat-panel__submit">
      <div class="create-twat-type">
        <label for="newTwatType"><strong>Type: </strong></label>
        <select id="newTwatType" v-model="state.selectedTwatType">
          <option :value="option.value" v-for="(option, index) in state.twatTypes" :key="index">
            {{ option.name }}
          </option>
        </select>
      </div>

      <button>
        Twat It!
      </button>
    </div>
  </form>
</template>

<script>
import { reactive, computed } from 'vue';

export default {
  name: "CreateTwatPanel",
  setup(props, ctx) {
    const state = reactive({
      newTwatContent: '',
      selectedTwatType: 'instant',
      twatTypes: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant Twat'}
      ]
    })

    const newTwatCharacterCount = computed(() => state.newTwatContent.length)

    function createNewTwat() {
      if (state.newTwatContent && state.selectedTwatType !== 'draft') {
        ctx.emit('add-twat', state.newTwatContent);
        state.newTwatContent = '';
      }
    }

    return {
      state,
      newTwatCharacterCount,
      createNewTwat
    }
  }
};
</script>

<style lang="scss" scoped>
.create-twat-panel {
  margin-top: 20px;
  padding: 20px 0;
  display: flex;
  flex-direction: column;

  textarea {
    border: 1px solid #DFE3E8;
    border-radius: 5px;
  }

  .create-twat-panel__submit {
    display: flex;
    justify-content: space-between;

    .create-twat-type {
      padding: 10px 0;
    }

    button {
      padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: aqua;
      color: black;
      font-weight: bold;
    }
  }

  &.--exceeded {
    color: red;
    border-color: red;

    .create-twat-panel__submit {
      button {
        background-color: red;
        color: white;
      }
    }
  }
}
</style>