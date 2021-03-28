<template>
  <div class="WorkoutCard">
    <h1 class="workoutCardDate">{{formattedDate(workout.date)}}</h1>
    <div class="workoutInfo">
      <div class="workoutExercise" v-for="(exercise, index) in workout.exercises" :key="index">
        <div v-if="exercise.type === 'benchpress'" class="exercise benchpress">
          <h1>Benchpress Exercise</h1>
          <p>Sets: {{exercise.sets}}</p>
          <p>Reps: {{exercise.reps}}</p>
          <p>Weight: {{exercise.weight}}</p>
        </div>
        <div v-if="exercise.type === 'running'" class="exercise running">
          <h1>Running Exercise</h1>
          <p>Distance: {{exercise.distance}}</p>
          <p>Time: {{exercise.time}}</p>
        </div>
      </div>
      <div class="deleteWorkoutCard" @click="$emit('delete:workout', myIndex)">Delete</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WorkoutCard',
  props: {
    workout: Object,
    myIndex: Number
  },
  methods: {
    formattedDate (d) {
      let newDate = new Date(d.replace(/-/g, '/'))
      let months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec']
      let month = months[newDate.getMonth()]
      let date = newDate.getDate()
      let year = newDate.getFullYear()
      let time = `${month} ${date}, ${year}`
      return time
    }
  },
  computed: {
    
  }
}
</script>

<style scoped>
.WorkoutCard {
  border: 1px solid rgb(156, 156, 156);
  border-radius: 7px;
  padding: 10px;
  overflow: hidden;
  box-shadow: 4px 4px 6px 1px rgba(0, 0, 0, 0.082); 
}
.workoutCardTitle {
  font-size: 22px;
  font-weight: bold;
}
.workoutCardDate {
  font-size: 22px;
  font-weight: bold;
}

.workoutInfo {
  font-size: 20px;
}
.workoutExercise {
  
}
.exercise {
  padding: 5px 0;
}
.exercise h1 {
  font-weight: bold;
}
.deleteWorkoutCard {
  cursor: pointer;
  color: rgb(160, 44, 44);
  font-size: 16px;
}
</style>