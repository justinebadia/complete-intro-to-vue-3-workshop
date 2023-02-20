<script>
export default {
  props: {
    character: {
      type: Object,
      required: true,
    },
  },
  emits: ["favorite"],
  methods: {
    addFavorite() {
      this.$emit("favorite", this.character);
    },
  },
};
</script>

<template>
  <div>
    <p>{{ character.name }}</p>
    <button v-if="!character.favorite" @click="addFavorite">Favorite</button>
  </div>
</template>
