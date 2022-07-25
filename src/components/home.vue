<template>
  <div class="container">
    <div class="side-bar">
      <h2 class="side-bar-title">Notes</h2>
      <div class="side-bar-item">
        {{ inputTitle }}
      </div>
    </div>
    <div class="main">
      <div class="main-input">
        <h2 class="main-title">Please Add Your note</h2>
        <input
          class="input"
          type="text"
          placeholder="Enter Title"
          v-model="inputTitle"
          v-if="!toggle"
        />
        <input
          class="description-input"
          type="text"
          placeholder="Enter Description"
          v-model="inputDescription"
          v-if="toggle"
        />
        <button @click="changeInput" class="add-note-button">
          Add {{ condition }}
        </button>
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
      toggle: false,
      condition: "Title",
    };
  },
  methods: {
    changeInput() {
      let input = document.querySelector(".input");
      let descInput = document.querySelector(".description-input");
      this.inputTitle = input.value;
      input.value = "";
      this.toggle = true;
      this.condition = "Description";
      this.inputDescription = descInput.value;
    },
  },
};
</script>

<style></style>
