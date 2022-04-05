<template>
  <div>
    <div class="btn-group" role="group">
      <button type="button" class="btn btn-outline-warning" @click="back()">
        Back
      </button>
      <h1>Edit</h1>
      <button type="button" class="btn btn-outline-warning" @click="update()">
        save
      </button>
    </div>

    <br />

    <input
      type="text"
      id="postTitle"
      v-model="title"
      :placeholder="post.postTitle + '...'"
    />
    <textarea v-model="msg" :placeholder="post.postMsg" id="postMsg"></textarea>
  </div>
</template>

<script>
import { updatePost } from "../firebase";
import postsData from "../data/Posts.json";

export default {
  name: "edit",
  data() {
    return {
      post: postsData[this.$route.params.post]||{postTitle:"Invalid",postMsg:"Invalid"},
      title: "",
      msg: ""
    };
  },
  created() {
    console.log("updating post " + this.post);
  },
  methods: {
    back() {
      this.$router.push("/account");
    },
    update() {
      updatePost(this.title, this.msg);
      alert("updated!");
      this.$router.push("/account");
    },
  },
};
</script>

<style scoped>
input,
textarea {
  width: 100%;
  text-align: center;
}
</style>
