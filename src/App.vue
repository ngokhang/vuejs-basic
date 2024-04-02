<template>
  <BaseLayout>
    <template #header>
      <HeaderComponent />
    </template>
  </BaseLayout>
</template>
<script>
import BaseLayout from "./layouts/BaseLayout.vue";
import HeaderComponent from "./components/HeaderComponent.vue";
import { computed } from "vue";

export default {
  components: { BaseLayout, HeaderComponent },
  data() {
    return {
      userList: [],
    };
  },
  inject: ["axios"],
  methods: {
    async fetchUsers() {
      this.userList = await this.axios.get("https://6484acbaee799e321626e9fe.mockapi.io/api/v1/users").then(res => res.data);
    },
  },
  created() {
    this.fetchUsers();
  },
  provide() {
    return {
      userList: computed(() => this.userList),
    };
  },
};
</script>
<style lang=""></style>
