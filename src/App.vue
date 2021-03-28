<template>
  <div class="App">
    <div class="workoutGrid">
      <workout-card v-for="(workout, index) in workouts" :key="index" :workout="workout" />
    </div>
    <add-workout-area @add:workout="addWorkout" />
  </div>
</template>

<script>
// menu that lets you choose between workouts / exercises
// filters for most distance / weight?
// list of workouts that is displayed in a card grid (1)
// click on card to display details
// list of exercises regardless of workouts
// add area. can add multiple exercises to a workout. once submitted, if the user wants to add more, they go to the workout. (2)
// auto set name of workout to date. if there are multiple in a day, then auto add 2 or time or something. (3)
// give users to change workout title? (4)

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
              type: 'benchpress', // types: running, bench press, custom?
              // note: 'Bench Press ',
              sets: 5,
              reps: 20,
              weight: 100
            },
            {
              type: 'running', // types: running, bench press, custom?
              // note: 'Running session ',
              time: 60, // in minutes?
              distance: 2.5 // in miles
            }
          ]
        },
        {
          date: '2021-03-16',
          exercises: [
            {
              type: 'benchpress', // types: running, bench press, custom?
              // note: 'Bench Press ',
              sets: 5,
              reps: 20,
              weight: 100
            },
            {
              type: 'running', // types: running, bench press, custom?
              // note: 'Running session ',
              time: 60, // in minutes?
              distance: 2.5 // in miles
            }
          ]
        }
      ]
    }
  },
  methods: {
    addWorkout (newWorkout) {
      console.log('Adding workout...')
      console.log(newWorkout)
      this.workouts.push(newWorkout)
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
  grid-gap: 10px;
  height: 100%;
}
.workoutGrid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 200px;

  grid-gap: 10px;
}
@media only screen and (max-width: 1200px) {
  .workoutGrid { grid-template-columns: repeat(2, 1fr); }
}
@media only screen and (max-width: 950px) {
  .workoutGrid { grid-template-columns: repeat(1, 1fr); }
}
</style>
