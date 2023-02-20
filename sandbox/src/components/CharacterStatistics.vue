<script>
export default {
  props: {
    characters: {
      type: Array,
      required: true,
    },
  },
  computed: {
    roleStatistics() {
      const roles = ["pirate", "capitaine", "docteur", "cuisinier"];
      const statistics = {
        pirate: 0,
        capitaine: 0,
        docteur: 0,
        cuisinier: 0,
      };
      this.characters.forEach((character) => {
        roles.forEach((role) => {
          if (character.role.indexOf(role) > -1) {
            statistics[role] += 1;
          }
        });
      });
      return statistics;
    },
  },
};
</script>

<template>
  <h2>Statistics</h2>
  <ul>
    <li v-for="(stat, role, index) in roleStatistics" :key="`role-${index}`">
      {{ role }}: {{ stat }}
    </li>
  </ul>
  <hr />
  <p>
    En string :
    <span v-for="(character, index) in characters" :key="`character-${index}`">
      {{ character.name }}{{ index === characters.length - 1 ? "" : ", " }}
    </span>
  </p>
</template>
