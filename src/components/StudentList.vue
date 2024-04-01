<template lang="">
  <div class="student-list">
    <div
      v-for="student in studentList"
      :key="student.id"
      class="student-list__item"
    >
      <p>{{ student.name }}</p>
      <input
        type="checkbox"
        @click="handleSelect(student.id)"
        v-model="student.selected"
      />
    </div>
  </div>
</template>
<script>
export default {
  props: {
    studentList: {
      type: Array,
      required: true,
    },
  },
  emits: {
    selectStudent: {
      type: Function,
      required: true,
    },
  },
  methods: {
    handleSelect(studentId) {
      this.$emit("selectStudent", this.studentList, studentId);
    },
  },
};
</script>
<style scoped>
.student-list {
  width: 300px;
  padding: 5px;
  border: 1px solid black;
}
.student-list__item {
  display: flex;
  gap: 10px;
}
</style>
