<template>
    <div class="home">
        <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
        <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
        <Notes></Notes>
    </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Notes from '../components/Notes.vue'

export default {
    name: 'home',
        components: {
        // HelloWorld,
            Notes
        }
    }
</script>