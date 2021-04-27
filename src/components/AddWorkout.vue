<template>
    <form @submit="onSubmit" class="add-form">
        <div class="form-control">
            <label>Workout</label>
            <input type="text" v-model="text" name="text" placeholder="Add new Workout to do and stay focus :)"/>
        </div>
        
        <div class="form-control">
            <label >Day & Time</label>
            <input type="text" v-model="day" name="day" placeholder="Add Day and Time"/>
        </div>
        <div class="form-control form-control-check">
            <label >Set Reminder</label>
            <input type="checkbox" v-model="reminder" name="reminder"/>
        </div>

        <input type="submit" value="Save Workout" class="btn btn-block">
    </form>
</template>


<script>
export default{
    name: 'AddWorkout',
    data(){
        return {
            text: '',
            day: '',
            reminder: false
        }
    },
    methods: {
        onSubmit(event){
            event.preventDefault()

            if(!this.text){
                alert('Trebuie sa adaugati un workout')
                return 
            }

            const new_workout = {
                text: this.text,
                day: this.day,
                reminder: this.reminder
            }

            console.log('Acesta este workoutul adaugat recent',new_workout)
            this.$emit('add-workout', new_workout)


            this.text = ''
            this.day = ''
            this.reminer = false

        }
    }

}
</script>

<style scoped>

.add-form {
    margin-bottom: 40px;
}

.form-control {
    margin: 20px;
}

.form-control label {
    display: block;
}

.form-control input {
    width: 100%;
    height: 40px;
    margin: 5px;
    padding: 10px;
    font-size: 14px;
}

.form-control-check {
    display: flex;
    align-items:flex-start;
    /* justify-content:c; */
}

.form-control-check label{
    flex: 1;
}

.form-control-check input{
    flex: 1;
    height: 20px;
}
</style>