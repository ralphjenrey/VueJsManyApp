

<template>
 <div class="text-center">
    <button class="btn btn-success" @click="showCalculator">Calculator</button>
    <button class="btn btn-warning" @click="showNotes">Notes</button>

    <HelloWorld v-if="showingCalculator" />
    <Notes v-if="showingNotes" />
    <NotesList v-if="showingNotes" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import Notes from './components/Notes.vue';
import NotesList from './components/NotesList.vue';
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/js/bootstrap.bundle.min.js';

  export default {
    components:{
      HelloWorld,
      Notes,
      NotesList,
    },
    data() {
    return {
    showingCalculator: false,
    showingNotes: false,
    };
  },
    methods: {
showCalculator() {
  this.showingCalculator = true;
  this.showingNotes = false;
},
showNotes() {
  this.showingCalculator = false;
  this.showingNotes = true;
},
    },
  };

</script>

<style scoped>

</style>
