<template>
    <div class="exercise-info-container">
        <table class="dummyData">
            <tr class="head table-row">
                <td> Exercise </td>
                <td class="headings"> Sets </td>
                <td class="headings"> Reps </td>
                <td class="headings"> Weight </td>
                <td> </td>

            </tr>
            <tr class="table-row" v-for="exercise in exercises" :key="exercise.id">
                <td v-if="editing === exercise.id">
                    <input type="text" v-model="exercise.name">
                    <input type="date" placeholder="mm-dd-yyyy" v-model="exercise.date">
                </td>
                <td v-else> <p class="exercise-name"> {{exercise.name}} </p><p class="date-alignment">{{exercise.date}}</p></td>
                <td v-if="editing === exercise.id">
                    <input type="text" v-model="exercise.sets">
                </td>
                <td v-else> <p class="exercise-sets"> {{exercise.sets}}</p></td>
                <td v-if="editing === exercise.id">
                    <input type="text" v-model="exercise.reps">
                </td>
                <td v-else> <p class="exercise-reps"> {{exercise.reps}} </p></td>
                <td v-if="editing === exercise.id">
                    <input type="text" v-model="exercise.weight">
                </td>
                <td v-else> <p class="exercise-weight"> {{exercise.weight}}</p></td>

                <td v-if="editing === exercise.id">
                    <button @click="$emit('save:exercise'(exercise.id))"> Save </button>
                </td>               
                <td v-else class="button-group">
                    <button class="btn-space btn-width" @click="editDisplay(exercise.id)"> Edit </button>
                    <button class="btn-width" @click="$emit('delete:exercise', exercise.id)"> Delete </button>
                </td>
            </tr>
        </table>
    </div>
</template>

<script>

export default {
    name: 'exerciseInfo',
    props: ['exercises'],
    methods: {
        editDisplay(id){
            this.editing = id
        },
        saveEdit(id) {
            
            let inputDate = this.exercises[id].date;
            console.log(inputDate);
            inputDate = inputDate.split('-');
            let newDate = inputDate[1] + "-" + inputDate[2] + "-" + inputDate[0]
            console.log(newDate)
            inputDate = newDate

            this.formattedDate = newDate;
            this.editing = null;
        }
    },
    data() {
        return {
            editing: null,
            formattedDate: null
        }
    }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.exercise-info-container{
    background:rgb(240, 240, 240);
}
.dummyData {
  padding: 1%;
  width: 100%;
  display:flex;
  flex-direction: column;
}

.table-row{
    padding:20px;
}
.exercise-name{
    font-weight: 700;
    text-align: left;
}
.exercise-sets{
    margin-right:4%;
}
.table-row{
    display:flex;
    justify-content: space-between;
    align-content: flex-start;
}
td{
    width:25%;
}
.headings{
    padding-left:6%;
}
tr.head{
    border-bottom: .5px solid grey;
    padding-bottom:10px;
}
.button-group{
    display:flex;
    align-items: center;
    justify-content: flex-end;
}
.btn-space{
    margin-right:15px;
}
.btn-width{
    width:59px;
}
.date-alignment{
    text-align: left;
}
</style>