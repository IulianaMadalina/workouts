<template>
    <div>
    <div v-if="show">
    <AddWorkout @add-workout="addWorkout"/>
    </div>

    <Workouts @toggle-reminder="toggleReminder" @delete-workout="deleteWorkout" :workouts="workouts"></Workouts>
    </div>
</template>


<script>

import Workouts from '@/components/Workouts'
import AddWorkout from '@/components/AddWorkout'

export default {
    name: 'Home',
    props: {
        showAddWorkout: Boolean
    },
    components:{
        Workouts,
        AddWorkout,
    },
    data(){
        return{
            workouts: []
        }
    },
    methods:{
        async deleteWorkout(id){
    console.log('Workout',id)
    if(confirm('Esti sigur/a ca vrei sa stergi acest workout?')){
        const res = await fetch(`api/workouts/${id}`, {
        method: 'DELETE'
        })

        res.status === 200 ?  (this.workouts=this.workouts.filter((workout)=> workout.id !== id)) : alert('Eroare la DELETE')


}
},

async toggleReminder(id){
    console.log('am dat dublu click pentru a schimba satrea reminderului',id)
    //update 
    
    const workoutToToggle = await this.fetchWorkout(id)
    const updateWorkout = {...workoutToToggle, reminder: !workoutToToggle.reminder}

    const res = await fetch(`api/workouts/${id}`,{
    method: 'PUT',
    headers: {
        'Content-type': 'application/json'
    },
    body: JSON.stringify(updateWorkout)
    })

    const data = await res.json()

    this.workouts=this.workouts.map((workout) => workout.id === id ? {...workout, reminder: data.reminder}: workout)
},

async addWorkout(workout){
    const res = await fetch('api/workouts', {
    method: 'POST',
    headers:{
        'Content-type' : 'application/json',
    
    },
    body: JSON.stringify(workout)
    })

    const data = await res.json()

    this.workouts=[...this.workouts,workout]
},

//async pt a rula 
async fetchWorkouts(){
    const res = await fetch('api/workouts')

    const data = await res.json()

    return data
},

async fetchWorkout(id){
    const res = await fetch(`api/workouts/${id}`)

    const data = await res.json()

    return data
}
},

async created() {
this.workouts= await this.fetchWorkouts()
}
}



</script>