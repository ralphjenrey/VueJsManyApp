<template>
  <div class="wrapper">
    <div class="container">
      <div class="nav">
        <button class="btn btn-warning me-2" @click="redo">Redo</button>
        <button class="btn btn-danger me-2" @click="undo">Undo</button>
        <button class="btn btn-primary me-2" @click="showNotes">Go to Notes</button>
        <button class="btn btn-primary" @click="showNotes">Back</button>
      </div>
      <textarea class="form-control" ref="textarea" v-if="!showingNotes"></textarea>
      <h1 v-if="showingNotes">Your Notes</h1>
      <NotesList :notes="notes" v-if="showingNotes"/>
      <button class="btn btn-primary" @click="addNote" v-if="!showingNotes">Add Notes</button>
    </div>
  </div>
</template>

<script>
import NotesList from './NotesList.vue';
export default {
  components: {
    NotesList
  },
  data() {
    return {
      notes: [],
      showingNotes: false,
      undoStack: [],
      redoStack: []
    };
  },
  methods: {
    addNote() {
      const text = this.$refs.textarea.value;
      this.notes.push(text);
      // Clear the redo stack when a new note is added
      this.redoStack = [];
    },
    showNotes() {
      this.showingNotes = !this.showingNotes;
    },
    undo() {
      if (this.notes.length > 0) {
        const removedNote = this.notes.pop();
        this.undoStack.push(removedNote);
      }
    },
    redo() {
      if (this.undoStack.length > 0) {
        const restoredNote = this.undoStack.pop();
        this.notes.push(restoredNote);
        this.redoStack.push(restoredNote);
      }
    }
  },
};
</script>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh; /* Adjust as needed */
}

textarea {
  height: 200px;
}
</style>
