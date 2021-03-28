<template>
  <div class="App">
    <div class="workoutGrid">
      <workout-card v-for="(workout, index) in workouts" :key="index" :myIndex="index" :workout="workout" @delete:workout="deleteWorkout" />
    </div>
    <add-workout-area @add:workout="addWorkout" />
  </div>
</template>

<script>
// reset css
import '@/reset.css'

import WorkoutCard from './components/WorkoutCard.vue'
import AddWorkoutArea from './components/AddWorkoutArea.vue'

export default {
  name: 'App',
  components: {
    WorkoutCard,
    AddWorkoutArea
  },
  data() {
    return {
      workouts: [
        {
          date: '2021-03-15',
          exercises: [
            {
              type: 'running', // types: running, bench press
              time: 60, // in minutes
              distance: 2.5 // in miles
            }
          ]
        },
        {
          date: '2021-03-16',
          exercises: [
            {
              type: 'benchpress', // types: running, bench press
              sets: 10,
              reps: 10,
              weight: 50
            },
            {
              type: 'running', // types: running, bench press
              time: 90, // in minutes
              distance: 4 // in miles
            }
          ]
        }
      ]
    }
  },
  methods: {
    addWorkout (newWorkout) {
      console.log('Adding workout...')
      this.workouts.push(newWorkout)
    },
    deleteWorkout (i) {
      console.log('Deleting workout...')
      this.workouts.splice(i, 1)
    }
  }
}
</script>

<style>
input, select, option {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
html, body {
  height: 100%;
}
.App {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: grid;
  grid-template-columns: auto 350px;
  height: 100%;
}
.workoutGrid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 300px;
  grid-gap: 10px;
  padding: 10px;
}
@media only screen and (max-width: 1200px) {
  .workoutGrid { grid-template-columns: repeat(2, 1fr); }
}
@media only screen and (max-width: 950px) {
  .workoutGrid { grid-template-columns: repeat(1, 1fr); }
}
</style>
