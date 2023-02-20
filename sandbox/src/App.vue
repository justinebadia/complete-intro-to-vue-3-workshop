<!-- single file components -->

<script>
import CharacterStatistics from "./components/CharacterStatistics.vue";
import CharacterCard from "./components/CharacterCard.vue";
import BaseLayout from "./components/BaseLayout.vue";

export default {
  components: {
    CharacterStatistics,
    CharacterCard,
    BaseLayout,
  },
  data: () => ({
    newCharacter: {
      name: "",
      favorite: false,
      role: [],
    },
    characters: [
      {
        name: "Luffy",
        favorite: false,
        role: ["pirate", "capitaine"],
      },
      {
        name: "Roronoa",
        favorite: false,
        role: ["pirate"],
      },
      {
        name: "Chopper",
        favorite: false,
        role: ["pirate", "docteur"],
      },
      {
        name: "Sanji",
        favorite: false,
        role: ["pirate", "cuisinier"],
      },
    ],
    favoriteList: [],
  }),
  methods: {
    addCharacterToList() {
      this.characters.push(this.newCharacter);
      this.newCharacter = { name: "" };
    },
    addFavoriteCharacter(payload) {
      this.favoriteList.push(payload);
      payload.favorite = true;
      console.log(this.favoriteList);
    },
  },
};
</script>

<!-- HTML de l'app -->
<template>
  <BaseLayout>
    <template v-slot:left>
      <h2>New characters</h2>
      <pre> {{ newCharacter }} </pre>
      <label for="character-name">Name</label>
      <input
        type="text"
        @keyup.enter="addCharacterToList()"
        v-model="newCharacter.name"
      />
    </template>

    <template v-slot:right>
      <CharacterStatistics v-bind:characters="characters" />
    </template>
  </BaseLayout>

  <p v-if="characters.length === 0">There are no characters</p>
  <ul v-else>
    <li v-for="(character, index) in characters" :key="`char-${index}`">
      <CharacterCard :character="character" @favorite="addFavoriteCharacter" />
    </li>
  </ul>

  <h2 v-if="favoriteList.length > 0">Favorite Characters</h2>

  <ul>
    <li v-for="(favorite, index) in favoriteList" :key="`fav-${index}`">
      {{ favorite.name }}
    </li>
  </ul>
</template>

<!-- manage the CSS -->
<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
