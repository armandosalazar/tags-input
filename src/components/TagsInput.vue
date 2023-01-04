<script>
export default {
  data() {
    return {
      newTag: "",
      tags: [],
    };
  },

  methods: {
    handleKeyDown(evt) {
      if (
        evt.key === "Backspace" &&
        this.newTag === "" &&
        this.tags.length > 0
      ) {
        this.tags.pop();
      }
      // const exist = this.tags.some(item => item === this.newTag);
      const exist = this.tags.includes(this.newTag);
      if (!exist) {
        if (evt.key === "Enter" && this.newTag !== "") {
          console.log("Enter pressed");
          this.tags.push(this.newTag);
          this.newTag = "";
        }
      } else {
        this.newTag = "";
      }
    },
    handleSubmit() {
      if (this.newTag !== "") {
        this.tags.push(this.newTag);
      }
    },
    handleDeleteTag(tag) {
      this.tags = this.tags.filter((t) => t !== tag);
    },
  },
};
</script>

<template>
  <h3>Tags Input</h3>
  <div class="tagsInput">
    <div class="tags">
      <div class="tag" v-for="(tag, index) in tags" :key="index">
        {{ tag }}
        <button @click="handleDeleteTag(tag)">x</button>
      </div>
    </div>
    <input type="text" v-model="newTag" @keydown="handleKeyDown" />
    <form @submit.prevent="handleSubmit" v-if="false">
      <input type="text" v-model="newTag" />
    </form>
  </div>
</template>

<style>
h3 {
  font-weight: bold;
}
</style>
