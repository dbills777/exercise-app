<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
  <div class="workout-container">
    <div class="timed">
      <form @submit.prevent="addCardio">
        <label>Cardio (with Distance)</label>
        <input v-model="cardio" name="cardio" placeholder="Cardio Activity" />
        <input v-model="duration" name="duration" type="number" placeholder="Duration" />
        <input v-model="distance" name="distance" type="number" placeholder="Distance" />
        <label class ="date-input" for="start">Workout Perfomed On:</label>
        <input  v-model="date" type="date" id="start" name="date" min="2021-03-01" max="2022-12-31" />
        <button>Add a New Exercise</button>
        <ul v-for="exercise in exercises" :key="exercise.id">
          <li>Workout Recorded On: {{ exercise.id.toDateString() }} {{ exercise.hours }}</li>
          <li>Exercise Name: {{ exercise.name }}</li>
          <li>Workout Date: {{ exercise.date }}</li>
          <li>Duration: {{ exercise.duration }} Minutes</li>
          <li>Distance: {{ exercise.distance }} Miles</li>
        </ul>
      </form>
    </div>
    <div class="timed">
      <form @submit.prevent="addAerobic">
        <label>Aerobic (no distance)</label>
        <input v-model="aerobic" name="aerobic" placeholder="Aerobic Activity" />
        <input v-model="aerobicDuration" name="aerobicDuration" type="number" placeholder="Duration" />
        <label class ="date-input2" for="start">Workout Perfomed On:</label>
        <input v-model="date" type="date" id="start" name="date" min="2021-03-01" max="2022-12-31" />
        <button>Add a New Exercise</button>
        <ul v-for="exercise in aerobicExercieses" :key="exercise.id">
          <li>Workout Recorded On: {{ exercise.id.toDateString() }} {{ exercise.hours }}</li>
          <li>Exercise Name: {{ exercise.name }}</li>
          <li>Workout Date: {{ exercise.date }}</li>
          <li>Duration: {{ exercise.aerobicDuration }} Minutes</li>
        </ul>
      </form>
    </div>
    <div class="weights">
      <form @submit.prevent="addWeights">
        <label>Strength Training</label>
        <input v-model="weightName" name="cardio" placeholder="Strength Training Activity" />
        <input v-model="sets" name="sets" type="number" placeholder="Sets" />
        <input v-model="reps" name="reps" type="number" placeholder="Reps" />
        <input v-model="weight" name="weight" type="number" placeholder="Weight" />
        <label for="start">Workout Perfomed On:</label>
        <input v-model="date" type="date" id="start" name="date" min="2021-03-01" max="2022-12-31" />
        <button>Add a New Exercise</button>
        <ul v-for="exercise in weightExercises" :key="exercise.id">
          <li>Workout Recorded On: {{ exercise.id.toDateString() }} {{ exercise.hours }}</li>
          <li>Exercise Name: {{ exercise.name }}</li>
          <li>Workout Date: {{ exercise.date }}</li>
          <li>Sets: {{ exercise.sets }}</li>
          <li>Reps: {{ exercise.reps }}</li>
          <li>Weight: {{ exercise.weight }} lbs</li>
        </ul>
      </form>
    </div>
  </div>
</template>

<script>
// import moment from 'moment'
import { ref } from 'vue';
const cardio = ref('');
const duration = ref('');
const date = ref('');
const distance = ref('');
const exercises = ref([]);
const aerobic = ref('');
const aerobicDuration = ref('');
const aerobicExercieses = ref([]);
const weightExercises = ref([]);
const sets = ref('');
const weightName = ref('');
const reps = ref('');
const weight = ref([]);

export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  // composition API
  setup() {
    function addCardio() {
      console.log('see date', date.value);
      exercises.value.push({
        date: date.value,
        name: cardio.value,
        duration: duration.value,
        distance: distance.value,
        id: new Date(),
        hours: new Date().toLocaleTimeString(),
        category: 'cardio',
      });
      cardio.value = '';
      duration.value = '';
      date.value = '';

    }
    function addAerobic() {
      console.log(aerobicExercieses.value);
      aerobicExercieses.value.push({
        name: aerobic.value,
        aerobicDuration: aerobicDuration.value,
        id: new Date(),
        hours: new Date().toLocaleTimeString(),
        category: 'aerobic',
        date: date.value,
      });
      aerobic.value = '';
      aerobicDuration.value = '';
      date.value = '';

    }
    function addWeights() {
      console.log(weightExercises.value);
      weightExercises.value.push({
        name: weightName.value,
        weight: weight.value,
        id: new Date(),
        hours: new Date().toLocaleTimeString(),
        category: 'weights',
        date: date.value,
        sets: sets.value,
        reps: reps.value,
      });
      aerobic.value = '';
      aerobicDuration.value = '';
      date.value = '';
    }
    return {
      addCardio,
      addAerobic,
      addWeights,
      exercises,
      cardio,
      aerobic,
      duration,
      distance,
      aerobicExercieses,
      weightExercises,
      date,
      aerobicDuration,
      sets,
      reps,
      weight,
      weightName,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.workout-container {
  margin: 3rem;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
form {
  display: flex;
  flex-direction: column;
  max-width: 30vw;
  margin: 0 auto;
}
label {
  margin-bottom: 1rem;
  color: rgb(77, 158, 77);
  font-weight: bold;
  text-transform: uppercase;
}
input {
  margin-bottom: 1rem;
}
button {
  padding: 0.5rem;
  background-color: rgb(110, 222, 110);
}
ul li {
  list-style-type: none;
  text-align: left;
}
.date-input{
  margin-top: 2.5rem;
}
.date-input2{
  margin-top: 4.5rem;
}
</style>
