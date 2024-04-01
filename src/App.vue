<template>
  <div class="wrapper">
    <StudentList :studentList="studentList" @selectStudent="selectStudent" />
    <div class="options">
      <button @click="moveToRight">Move to right</button>
      <button @click="moveToLeft">Move to left</button>
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
          @click="selectStudent(studentListFiltered, student.id)"
          v-model="student.selected"
        />
      </div>
    </div>
  </div>
</template>
<script>
import StudentList from "./components/StudentList.vue";
export default {
  components: {
    StudentList,
  },
  data() {
    return {
      studentList: [
        { id: 1, name: "Ngô Phú Khang", age: 21, selected: false },
        { id: 2, name: "Nguyễn Thị Linh", age: 21, selected: false },
        { id: 3, name: "Nguyễn Thị Hồng", age: 21, selected: false },
        { id: 4, name: "Bùi Thu Quỳnh", age: 21, selected: false },
      ],
      studentListFiltered: [],
    };
  },
  methods: {
    selectStudent(arrayStudent, studentId) {
      arrayStudent = arrayStudent.map((student) =>
        student.id === studentId
          ? { ...student, selected: !student.selected }
          : student,
      );
    },
    moveToRight() {
      this.studentListFiltered = this.studentList.reduce(
        (acc, curr) => {
          if (curr.selected) {
            acc.push({ ...curr, selected: false });
          }
          return acc;
        },
        [...this.studentListFiltered],
      );
      this.studentList = this.studentList.filter(
        (student) => !student.selected && { ...student, selected: false },
      );
    },
    moveToLeft() {
      this.studentList = this.studentListFiltered.reduce(
        (acc, curr) => {
          if (curr.selected) {
            acc.push({ ...curr, selected: false });
          }
          return acc;
        },
        [...this.studentList],
      );

      this.studentListFiltered = this.studentListFiltered.filter(
        (student) => !student.selected && { ...student, selected: false },
      );
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
</style>
