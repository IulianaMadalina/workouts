<template>
<div>
    <div :key="workout.id" v-for="workout in workouts">
        <Workout @toggle-reminder="$emit('toggle-reminder', workout.id)" @delete-workout="$emit('delete-workout',workout.id)" :workout="workout"/>
    </div>
</div>
</template>

<script>
import Workout from '../components/Workout'

export default {
    name :'Workouts',
    props:{
        workouts: Array,
    },
    components: {
        Workout,
    },
    //array of events emits
    emits:['delete-workout', 'toggle-reminder']

}
</script>