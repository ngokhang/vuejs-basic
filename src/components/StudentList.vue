<template>
  <div class="wrapper">
    <div class="student-list">
      <div
        v-for="student in studentList"
        :key="student.id"
        class="student-list__item"
      >
        <p>{{ student.name }}</p>
        <input
          type="checkbox"
          @click="handleSelect(this.studentList, student.id)"
          v-model="student.selected"
        />
      </div>
    </div>
    <div class="options">
      <button @click="handleMoveToRight()">Move to right</button>
      <button @click="handleMoveToLeft()">Move to left</button>
      <button @click="console.log(studentListFiltered)">View</button>
    </div>
    <div class="students-selected">
      <div
        v-for="student in studentListFiltered"
        :key="student.id"
        class="students-selected__item"
      >
        <p>{{ student.name }}</p>
        <input
          type="checkbox"
          @click="handleSelect(this.studentListFiltered, student.id)"
          v-model="student.selected"
        />
      </div>
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
    studentListFiltered: {
      type: Array,
      required: true,
    },
  },
  emits: {
    selectStudent: {
      type: Function,
      required: true,
    },
    moveToRight: {
      type: Function,
      required: true,
    },
    moveToLeft: {
      type: Function,
      required: true,
    },
  },
  methods: {
    /**
     *
     * @param {*} arrayStudent
     * @param {*} studentId
     *
     * arrayStudent: Present the list of students, such as studentList or studentListFiltered
     * studentId: The id of the student that you want to select
     */
    handleSelect(arrayStudent, studentId) {
      this.$emit("selectStudent", arrayStudent, studentId);
    },
    handleMoveToRight() {
      this.$emit("moveToRight");
    },
    handleMoveToLeft() {
      this.$emit("moveToLeft");
    },
  },
};
</script>
<style scoped>
.wrapper {
  display: flex;
  gap: 40px;
}
.options {
  width: 200px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 20px;
  padding: 5px;
  border: 1px solid black;
}
.students-selected {
  width: 300px;
  padding: 5px;
  border: 1px solid black;
}
.students-selected__item {
  display: flex;
  gap: 10px;
}
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
