<template>
  <div id="app">
    <!--Recieves new student data from the newStudentForm, feeds the new student data to newStudentAdded()-->
    <NewStudentForm v-on:student-added="newStudentAdded"></NewStudentForm>
    <!--Feeds students array to StudentTable, listens for student-present and delete-student-->
	  <StudentTable v-bind:students="students" 
	  v-on:student-present="studentArrivedOrLeft"
	  v-on:delete-student="studentDeleted"></StudentTable>
    <!--Sends message and name to StudentMessage-->
	  <StudentMessage v-bind:message="message" v-bind:name="name"></StudentMessage>
  </div>
</template>

<script>
  import NewStudentForm from './components/NewStudentForm.vue'
  import StudentTable from './components/StudentTable.vue'
  import StudentMessage from './components/StudentMessage.vue'

  export default {
    name: 'app',
    data() {
      return{
        students:[],
	    message: "",
	    name: ""
	  }
    },
    components: {
      NewStudentForm,
	  StudentTable,
	  StudentMessage
    },
    methods: {
      newStudentAdded(student) {
        //pushes the new student onto the students array and sorts the array alphabetically.
        this.students.push(student)
        this.students.sort(function(s1,s2){
          return s1.name.toLowerCase() > s2.name.toLowerCase() ? 1 : -1
        })
	  },
	  studentArrivedOrLeft(student){
      //prepares a message and name to send to StudentMessage
		  this.message = student.present ? "Welcome, " : "Goodbye, "
		  this.name = student.name
	  },
	  studentDeleted(student){
      //Makes a new array from the students array that includes everything but the selected student inorder to cull said student.
		  this.students = this.students.filter( function(s) {return s != student})
	  }
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
