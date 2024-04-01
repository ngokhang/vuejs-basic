<template>
  <div class="wrapper">
    <StudentList
      :studentList="studentList"
      :studentListFiltered="studentListFiltered"
      @selectStudent="selectStudent"
      @moveToLeft="moveToLeft"
      @moveToRight="moveToRight"
    />
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
<style scoped></style>
