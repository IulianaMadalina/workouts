<template>
    <header>
        <h1>{{title}}</h1>
        <Button v-show="homePage" @btn-click="$emit('toggle-add-workout')" :text="showAddWorkout ? 'Close' : 'Add Workout'" 
        :color="showAddWorkout ? '#EDC9AF' : 'pink'"/>
        
    </header>
</template>

<script>
import Button from './Button'
export default {
    name:'Header',
    props: {
        title: {
            type: String,
            default:'Aplicatie Vue'
        },
        showAddWorkout: Boolean
    },
    components: {
        Button
    },
    //reactivitate = 
    computed: {
        homePage(){
            if(this.$route.path === '/') {
                return true
            }
            else 
            {
                return false
            }
        }

    }
}
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30px;
}
</style>