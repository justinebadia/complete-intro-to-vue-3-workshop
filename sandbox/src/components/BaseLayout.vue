<template>
  <div class="grid">
    <div>
      <slot class="left" name="left" />
    </div>
    <div>
      <slot name="right" />
    </div>
  </div>
</template>

<style>
.grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  border: 5px solid rgb(110, 76, 175);
}
</style>
