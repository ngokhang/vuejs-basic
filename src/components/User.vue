<template lang="">
  <div>
    {{ userData.name }}
  </div>
</template>
<script>
export default {
  props: {
    userData: {
      type: {
        name: String,
        avatar: String,
        id: Number,
      },
      required: true,
    },
  },
};
</script>
<style lang=""></style>
