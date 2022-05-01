<template>
  <InputExercises 
  @add:exercise="storeExercise"
  />
  <ExerciseInfo 
  :exercises="Exercises"
  @delete:exercise="deleteExercise"
  @edit:exercise="editExercise"
  />
</template>

<script>
import InputExercises from './components/InputExercises.vue'
import ExerciseInfo from './components/ExerciseInfo.vue'

export default {
  name: 'App',
  components: {
    InputExercises,
    ExerciseInfo,
  },
  data() {
    return {
      Exercises: [
        {
          name: "Bicep Curl",
          date: '2022-02-03',
          sets: 5,
          reps: 12,
          weight: "30 lbs",
          id: 0
        },
        {
          name: "Situps",
          date: '01-20-2022',
          sets: 3,
          reps: 25,
          weight: null,
          id: 1
        },
        {
          name: "Lat Pulldown",
          date: '01-20-2022',
          sets: 3,
          reps: 15,
          weight: "45 lbs",
          id: 2
        },
        {
          name: "Hammer Curl",
          date: '01-20-2022',
          sets: 3,
          reps: 10,
          weight: "20 lbs",
          id: 3
        },
      ]
    }
  },
  methods: {
    storeExercise(exercise) {
        let lastId = this.Exercises.length;
        lastId > 0 ? lastId + 1 : lastId = 0;
        let id = lastId
        const newExercise = {...exercise, id};
        newExercise.reps = parseInt(newExercise.reps);
        newExercise.sets = parseInt(newExercise.sets);
        newExercise.weight = parseInt(newExercise.weight)

        let result = this.typeCheck(newExercise);

        if (result === true){
          return
        }else if (result === false){

          if (isNaN(newExercise.weight)) {
            newExercise.weight = " ";
            this.Exercises = [...this.Exercises, newExercise];
          } else{
          newExercise.weight = newExercise.weight + " lbs"
          this.Exercises = [...this.Exercises, newExercise]
          }
        }
    },
    typeCheck(exercise){
      let name = exercise.name;
      let set = exercise.sets;
      let rep = exercise.reps;
      let weight = exercise.weight;
      let errOccurredBool = false;

      if(set === Number || name === String || rep === Number || set === Number || weight === Number){
        alert('You must enter in letters for the Exercise Name and Numbers for the amount of Sets, Reps, and Weight values.')
        errOccurredBool = true;
      }
      return(errOccurredBool)
    },
    deleteExercise(id){
      this.Exercises = this.Exercises.filter(exercise => exercise.id !== id)
    },
    editExercise(id, updatedItem){
      this.Exercises = this.Exercises
      .map(exercise =>  {
        return exercise.id === id ? updatedItem : true;
      })
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  border-left:black 1px solid;
  border-right:black 1px solid;
  border-top:black 1px solid;
}
body {
  max-width: 1000px;
  margin:0 auto;
}
.exerciseInfo {
  background:rgb(233, 233, 233);
  text-align: left;
  display:grid;
}
</style>
