<template>
  <div class="AddWorkoutArea">
    <h1>Add workout</h1>
    
    <form @submit.prevent="formSubmit">
      <label for="workoutDate">Date: </label>
      <input v-model="date" type="date" name="workoutDate">
      <div class="exerciseList">
        <div class="exerciseItem" v-for="(exercise, index) in exercises" :key="index" >
          <label for="exerciseSelect">Excercise type: </label>
          <select v-model="exercise.type" name="exerciseSelect">
            <option value="benchpress">Benchpress</option>
            <option value="running">Running</option>
          </select>
          <div v-if="exercise.type === 'benchpress'" class="benchpressAdd exerciseItemParams">
            <input v-model="exercise.sets" placeholder="Sets" type="text" required>
            <input v-model="exercise.reps" placeholder="Reps" type="text" required>
            <input v-model="exercise.weight" placeholder="Weight" type="text" required>
          </div>
          <div v-if="exercise.type === 'running'" class="runningAdd exerciseItemParams">
            <input v-model="exercise.distance" placeholder="Distance" type="text" required>
            <input v-model="exercise.time" placeholder="Time" type="text" required>
          </div>
          <button type="button" @click="deleteWorkout(index)">Delete</button>
        </div>
        <button type="button" @click="addWorkout">Add Exercise in Workout</button>
        
      </div>
      
      <button type="submit">Add Workout</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'AddWorkoutArea',
  data() {
    return {
      date: null,
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
    }
  }
}
</script>

<style scoped>
.AddWorkoutArea {
  border: 1px solid black;
}
</style>