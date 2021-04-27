<template>
    <div
    @dblclick="$emit('toggle-reminder', workout.id)" :class="[workout.reminder ? 'reminder' : '' ,'workout']">
        <h3>{{ workout.text }}</h3>
        <i v-on:click="$emit('delete-workout',workout.id)" class="fas fa-times"></i>
        <p>{{ workout.day }}</p>
    </div>
</template>

<script>

export default {
    name: 'Workout',
    props: {
        workout: Object,
    },
    // methods: {
    //     onDelete(id){
    //         console.log("Workout programat sters",id)
    //         this.$emit('delete-workout', id)
    //     }
    // }
}

</script>

<style scoped>
.fas {
    color:red;
}

.workout {
    background: white;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
}

.workout.reminder {
    border-left: 5px solid blue;
}

.workout h3{
    display: flex;
    align-items: center;
    justify-content: space-between;
}

</style>