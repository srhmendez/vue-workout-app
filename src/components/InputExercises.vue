<template>

  <div class="inputArea-all-inputs">
      <form @submit.prevent="handleSubmit" class="exercise-form">
        <div id="name-container">
            <div class="input-group">
                <label for="exercise-name">Exercise:</label>
                <input type="text" id="exercise-name" v-model="exercise.name"><br><br>
            </div>      
        </div>
        <div id="rep-container">
          <div class="input-group">
              <label for="exercise-rep">Reps:</label>
              <input type="text" id="exercise-rep" v-model="exercise.reps"><br><br>
          </div>
        </div>
        <div id="sets-container">
            <div class="input-group">
                <label for="weight">Sets:</label>
                <input type="text" id="sets" v-model="exercise.sets"><br><br>
            </div>
        </div>
        <div id="weights-container">
            <div class="input-group">
                <label for="weight">Weight:</label>
                <input type="text" id="weight" v-model="exercise.weight"><br><br>
            </div>
        </div>
        <div class="inputArea">
            <input class="submitBtn" type="submit" value="Add Exercise" @submit="handleSubmit">
        </div>        
      </form>
  </div>

</template>

<script>


export default {
    name:'input-exercise-info',
    data() {
      return {
        exercise: {
          name: '',
          reps: '',
          sets: '',
          weight: '',
        }
      }
    },
    methods: {
        handleSubmit() {
            this.$emit('add:exercise', this.exercise)
            this.exercise = {
                name: '',
                reps: '',
                sets: '',
                weight: '',
            }
        }
    }


}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

form.exercise-form{
    display:flex;
    flex-direction: row;
    width:100%;
    justify-content:space-between;
    align-items: center;
}
.inputArea-all-inputs{
  padding:2%;
}

/* Name Input Styling */
#name-container{
    width:100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-content: center;
}
#exercise-name{
    margin-left:2%;
}

/* Rep Input Styling */
#rep-container{
    width:100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-content: center;
}
#exercise-rep{
    margin-left:2%;
}
.input-group{
    text-align: left;
}
/* Sets Input Styling */
#sets-container{
    width:100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-content: center;
}
#sets{
    margin-left:2%;
}

/* Weights input styling */
#weights-container{
    width:100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-content: center;
}
#weight{
    margin-left:2%;
}

label{
    margin-left:2%;
}
/* Submit button styling */
.submitBtn {
    border-radius:8px;
    background-color:rgb(47, 100, 180);
    color:white;
    border:none;
    padding:3% 4.5%;
}
.inputArea{
    width:90%;
    display:flex;
    justify-content: center;
    align-content: center;
}
</style>