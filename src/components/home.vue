<template>
  <div class="container">
    <div class="side-bar">
      <h2 class="side-bar-title">Notes</h2>
      <h4 style="color: #c937ae" v-if="notes.length < 1">No Notes Yet</h4>
      <ul>
        <li class="side-bar-item" v-for="note in notes" :key="note.index">
          <!-- In this section i get note.id for my method which is down in methods section -->
          <p @click="btn(note.id)">
            {{ note.title }}
            <button class="remove-button" @click="rembtn(note.id)">x</button>
          </p>
        </li>
      </ul>
    </div>
    <div class="main">
      <div class="main-input">
        <h2 class="main-title">Please Add Your note</h2>
        <input
          class="input"
          type="text"
          placeholder="Enter Title"
          v-model="inputTitle"
        />
        <input
          class="description-input"
          type="text"
          placeholder="Enter Description"
          v-model="inputDescription"
        />
        <button @click="addMethod" class="add-note-button">Add Note</button>
      </div>
      <div class="information">
        <h2>{{ infoTitle }}</h2>
        <br />
        <h4>{{ infoDescription }}</h4>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomePage",

  data() {
    return {
      inputTitle: null,
      inputDescription: null,
      notes: [],
      infoTitle: null,
      infoDescription: null,
    };
  },

  methods: {
    //The main method to make the notes array of objects and store the data
    addMethod() {
      if (this.inputTitle != null) {
        this.notes.push({
          id: this.notes.length,
          title: this.inputTitle,
          description: this.inputDescription,
        });
        this.inputTitle = null;
        this.inputDescription = null;
        let titleInput = document.querySelector(".input");
        titleInput.style = "border-bottom : 1px solid black";
      }
      //Here We prevent from Spaming the notes and user will have to put title at least
      else if (this.inputTitle === null) {
        let titleInput = document.querySelector(".input");
        titleInput.style = "border-bottom : 1px solid red";
      }
    },
    //With the note.id that ive got now i can know which note the user has selected and to the work  whit it
    btn(index) {
      let selectedNote = this.notes[index];
      this.infoTitle = selectedNote.title;
      this.infoDescription = selectedNote.description;
    },
    rembtn(index) {
      this.notes.splice(index, 1);
    },
  },
  //This Whole Section is for adding local storage to my project
  mounted() {
    if (localStorage.notes) {
      this.notes = JSON.parse(localStorage.notes);
    }
  },
  watch: {
    notes(newNotes) {
      localStorage.notes = JSON.stringify(newNotes);
    },
  },
};
</script>

<style></style>
