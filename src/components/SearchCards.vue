<template>
  <h3>Search Cards</h3>

  <form @submit.prevent="handleSubmit">
    <input v-model="val" type="text" />
    <button type="submit">Submit</button>
    <div>
      <ul></ul>
    </div>
  </form>
</template>

<script>
import { ref, reactive, toRefs } from "vue";
import axios from "axios";

export default {
  setup() {
    const val = ref("");
    const cards = reactive({ list: [] });
    const handleSubmit = async () => {
      console.log(val.value);
      const response = await axios.get(
        `https://api.magicthegathering.io/v1/cards?name=${val.value}`
      );
      console.log(response.data.cards);
      cards.list = ref(response.data.cards);
      console.log("cards.list", cards.list);
    };
    return { val, cards, ...toRefs(cards), handleSubmit };
  },
};
</script>

<style>
</style>