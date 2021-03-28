<template>
  <div class="AddWorkoutArea">
    <h1>Add workout</h1>
    
    <form @submit.prevent="formSubmit">
      <div class="dateInfo">
        <label for="workoutDate">Date: </label>
        <input v-model="date" type="date" name="workoutDate" required>
      </div>
      
      <div class="exerciseList">
        <div class="exerciseItem" v-for="(exercise, index) in exercises" :key="index" >
          <label for="exerciseSelect">Excercise type: </label>
          <select v-model="exercise.type" name="exerciseSelect">
            <option value="benchpress">Benchpress</option>
            <option value="running">Running</option>
          </select>
          <div v-if="exercise.type === 'benchpress'" class="benchpressAdd exerciseItemParams">
            <div class="paramInput">
              <label for="sets">Sets: </label>
              <input v-model="exercise.sets" placeholder="Sets" name="sets" type="text" required>
            </div>
            <div class="paramInput">
              <label for="reps">Reps: </label>
              <input v-model="exercise.reps" placeholder="Reps" name="reps" type="text" required>
            </div>
            <div class="paramInput">
              <label for="text">Weight: </label>
              <input v-model="exercise.weight" placeholder="Weight" name="weight" type="text" required>
            </div>
          </div>
          <div v-if="exercise.type === 'running'" class="runningAdd exerciseItemParams">
            <div class="paramInput">
              <label for="distance">Distance: </label>
              <input v-model="exercise.distance" placeholder="Distance" name="distance" type="text" required>
            </div>
            <div class="paramInput">
              <label for="time">Time: </label>
              <input v-model="exercise.time" placeholder="Time" name="time" type="text" required>
            </div>
          </div>
          <div class="deleteButton" type="button" @click="deleteWorkout(index)">Delete</div>
        </div>
        <div class="addExerciseButton" type="button" @click="addWorkout">+ Add Exercise</div>
        
      </div>
      
      <button class="addWorkoutButton" type="submit">Submit Workout</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'AddWorkoutArea',
  data() {
    return {
      date: this.currentDate(),
      exercises: [
        {
          type: 'benchpress',
          sets: 20,
          reps: 20,
          weight: 180
        },
        {
          type: 'running',
          distance: 2,
          time: 60
        }
      ]
    }
  },
  methods: {
    formSubmit () {
      this.$emit('add:workout', this.filteredWorkout)
      this.exercises = [{ type:'benchpress' }]
    },
    addWorkout () {
      console.log('addWorkout')
      this.exercises.push({type:'benchpress'})
    },
    deleteWorkout (index) {
      console.log(index)
      this.exercises.splice(index, 1)
    },
    currentDate () {
      let curDate = new Date()
      let month = ("0" + (curDate.getMonth() + 1)).slice(-2)
      let date = curDate.getDate()
      let year = curDate.getFullYear()
      let time = `${year}-${month}-${date}`
      return time
    }
  },
  computed: {
    filteredWorkout: function () {
      // returns the exercise object without unneeded fields for it's type
      return {
        date: this.date,
        exercises: this.exercises.map(exercise => {
          if (exercise.type === 'benchpress') {
            return {
              type: exercise.type,
              sets: exercise.sets,
              reps: exercise.reps,
              weight: exercise.weight
            }
          }
          else if (exercise.type === 'running') {
            return {
              type: exercise.type,
              distance: exercise.distance,
              time: exercise.time
            }
          }
          return false
        })
      }
    },
    currentDate2: function () {
      let curDate = new Date()
      console.log(curDate)
      let month = curDate.getMonth()
      console.log(month)
      let date = curDate.getDate()
      let year = curDate.getFullYear()
      let time = `${year}/${month}/${date}`
      return time
    }
  }
}
</script>

<style scoped>
.AddWorkoutArea {
  border-left: 1px solid rgb(155, 155, 155);
  padding: 10px;
}
.AddWorkoutArea h1 {
  font-size: 32px;
  font-weight: bold;
}
.AddWorkoutArea form {

}


.dateInfo {
  padding-top: 10px;
}
.dateInfo label[for="workoutDate"] {
  
}
.dateInfo input[name="workoutDate"] {

}

.exerciseList {
  padding: 10px 0;
  font-size: 20px;
}
.exerciseList .exerciseItem {
  border-top: 1px solid rgb(199, 199, 199);
  padding: 10px 0;
}
label[for="exerciseSelect"] {
  margin-bottom: 10px;
}
select[name="exerciseSelect"] {
  font-size: 16px;
  margin-bottom: 5px;
}
.exerciseItemParams {

}
.exerciseItemParams .paramInput {
  display: block;
  padding: 5px 0;
}
.exerciseItemParams .paramInput input[type="text"] {
  width: 50px;
  font-size: 16px;
}

.deleteButton {
  cursor: pointer;
  color: rgb(160, 44, 44);
}
.deleteButton:hover {
  color: rgb(109, 10, 10);
}
.addExerciseButton {
  cursor: pointer;
}
.addWorkoutButton {
  padding: 5px 15px;
  font-size: 20px;
  border: none;
  border-radius: 5px;
  background-color: rgb(75, 75, 75);
  color: white;
}
</style>