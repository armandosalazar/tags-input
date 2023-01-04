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
  <h2>
    Tags Input<span class="material-symbols-outlined tag-icon">sell</span>
  </h2>
  <div class="tagsInput">
    <div class="tags">
      <div class="tag" v-for="(tag, index) in tags" :key="index">
        {{ tag }}
        <span
          class="material-symbols-outlined small-icon"
          @click="handleDeleteTag(tag)"
        >
          close
        </span>
      </div>
    </div>
    <input type="text" v-model="newTag" @keydown="handleKeyDown" />
    <form @submit.prevent="handleSubmit" v-if="false">
      <input type="text" v-model="newTag" />
    </form>
  </div>
</template>

<style>
/* * {
  outline: 1px dashed #ccc;
} */

h2 {
  margin-top: 20px;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
}

.tagsInput {
  padding: 1rem 2rem;
  /* max-width: min-content; */
  width: 500px;
  /* border: 1px solid #ccc; */
  border-radius: 5px;
  margin: 20px auto;
  box-shadow: 0 0 5px #ccc;
}

.tags {
  display: flex;
  flex-wrap: wrap;
}

.tag {
  background-color: #e8dff8;
  margin: 1px 2px;
  padding: 5px 10px;
  display: flex;
  align-items: center;
  border-radius: 5px;
}

.small-icon {
  font-size: 1rem;
  cursor: pointer;
  margin-left: 2px;
}

.tag-icon {
  margin-left: 5px;
}

.tagsInput input {
  border: none;
  /* outline: none; */
  outline: 1px solid #e7e0ec;
  width: 100%;
  margin-top: 10px;
  /* font-size: 1rem; */
  border-radius: 5px;
  padding: 5px 10px;
}
</style>
