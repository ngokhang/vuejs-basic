<template>
  <header>Day la header</header>
  <button @click="console.log(userList)">Log user list</button>
</template>
<script>
export default {
  inject: ["userList"],
};
</script>
<style lang=""></style>
