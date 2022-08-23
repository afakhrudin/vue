<template>
  <div class="container">
    <div v-if="User">
      <p>Hi {{ User }}</p>
    </div>
    <div>
      <form @submit.prevent="submit">
        <div>
          <label for="title">Title:</label>
          <input type="text" name="title" v-model="post.title" />
        </div>
        <div>
          <textarea
            name="write_up"
            v-model="post.write_up"
            placeholder="Write up..."
          ></textarea>
        </div>
        <button type="submit">Submit</button>
      </form>
    </div>
    <div class="posts" v-if="Posts">
      <ul>
        <li v-for="post in Posts" :key="post.id">
          <div id="post-div">
            <p>{{ post.title }}</p>
            <p>{{ post.write_up }}</p>
            <p>Written By: {{ post.author.username }}</p>
            <router-link :to="{name : 'editPosts', params: {id : post.id}}">Edit</router-link>
            <button @click="deletePosts(post)" style="margin-left: 20px;">delete</button>
          </div>
        </li>
      </ul>
    </div>
    <div v-else>Oh no!!! We have no posts</div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
  name: "Posts",
  components: {},
  data() {
    return {
      post: {
        title: "",
        write_up: "",
      },
    };
  },
  created: function() {
    // a function to call getposts action
    this.GetPosts()
  },
  computed: {
    ...mapGetters({ Posts: "StatePosts", User: "StateUser" }),
  },
  methods: {
    ...mapActions(["CreatePost", "GetPosts"]),
    async submit() {
      try {
        await this.CreatePost(this.post);
      } catch (error) {
        throw "Sorry you can't make a post now!"
      }
    },
    deletePosts(post){
      this.$store.dispatch('deletePosts', post);
    }
  },
};
</script>
<style scoped>
* {
  box-sizing: border-box;
}

label {
  padding: 12px 12px 12px 0;
  display: inline-block;
}

button[type="submit"] {
  background-color: #4caf50;
  color: white;
  padding: 12px 20px;
  cursor: pointer;
  border-radius: 30px;
  margin: 10px;
}

button[type="submit"]:hover {
  background-color: #45a049;
}

input {
  width: 60%;
  margin: 15px;
  border: 0;
  box-shadow: 0 0 15px 4px rgba(0, 0, 0, 0.06);
  padding: 10px;
  border-radius: 30px;
}

textarea {
  width: 75%;
  resize: vertical;
  padding: 15px;
  border-radius: 15px;
  border: 0;
  box-shadow: 0 0 15px 4px rgba(0, 0, 0, 0.06);
  height: 150px;
  margin: 15px;
}

ul {
  list-style: none;
}

#post-div {
  border: 3px solid #000;
  width: 500px;
  margin: auto;
  margin-bottom: 5px;
}
</style>
