<template>
<v-btn color="primary" class="button-done-sorting" @click="$store.commit('toggleSorting')">
  Done Sorting
</v-btn>
</template>

<script>
export default {
  name: "ButtonDoneSorting"
}
</script>

<style lang="sass">
.button-done-sorting
  position: fixed
  bottom: 20px
  left: 50%
  transform: translateX(-50%)

</style>