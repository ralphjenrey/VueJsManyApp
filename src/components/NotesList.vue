<template>
  <div class="notes-list">
    <ul class="list-group">
      <li v-for="note in notes" :key="note" class="list-group-item position-relative">
        <div @click="showRemainingChars(note)" class="fw-bold" contenteditable>{{ note.slice(0, 40) }}{{ note.length > 40 ? '...' : '' }}         </div>
        <button class="btn btn-danger btn-sm position-absolute top-0 end-0" @click="handleRemoveNoteClick(note)">
          X
        </button>
      </li>
    </ul>
    <textarea v-if="selectedNote" class="remaining-chars-textarea">{{ selectedNote }}</textarea>
  </div>
</template>

<script>
export default {
  props: ['notes'],
  data() {
    return {
      selectedNote: null,
    };
  },
  methods: {
    handleRemoveNoteClick(note) {
      this.removeNote(note);
      this.hideRemainingChars();
    },
    removeNote(note) {
      const index = this.notes.indexOf(note);
      if (index !== -1) {
        this.notes.splice(index, 1);
      }
    },
    showRemainingChars(note) {
      if (this.selectedNote === note) {
        // If the clicked note is already selected, hide it
        this.selectedNote = null;
      } else {
        // Otherwise, show the remaining characters of the clicked note
        this.selectedNote = note;
      }
    },
    hideRemainingChars() {
      // Hide the remaining characters when the textarea is clicked
      this.selectedNote = null;
    },
  },
};
</script>

<style scoped>
.remaining-chars-textarea {
  width: 100%;
  height: 100px;
  margin-top: 10px;
}
</style>
