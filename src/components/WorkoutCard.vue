<template>
  <div class="WorkoutCard">
    <h1 class="workoutCardTitle">{{workout.name}}</h1>
    <p>{{workout.date}}</p>
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
    </div>
  </div>
</template>

<script>
export default {
  name: 'WorkoutCard',
  props: {
    workout: Object
  },
  methods: {
    
  }
}
</script>

<style scoped>
.WorkoutCard {
  border: 1px solid black;
  border-radius: 7px;
  padding: 5px;
  cursor: pointer;
}
.WorkoutCard:hover {
  background-color: rgb(241, 241, 241);
}
.workoutCardTitle {
  font-size: 22px;
  font-weight: bold;
}

.workoutInfo {
  
}
.workoutExercise {
  
}
.exercise {
  padding: 5px 0;
}
.exercise h1 {
  font-weight: bold;
}
</style>