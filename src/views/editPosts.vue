<template>

	<div class="container">

		<div>
			<label for="title">Title:</label> <br>
			<input type="text" name="title" v-model="post.title" />
		</div><br>
		<div>
			<textarea
			name="write_up"
			v-model="post.write_up"
			placeholder="Write up..."
			></textarea>
		</div>
		<button type="submit">Edit</button>

	</div>

</template>

<script>
import { mapState } from "vuex";


export default {

	name: 'editPosts',

	methods: {
		...mapState(["posts"]),
		post(){
			return this.posts.find(data => data.id == this.$route.params.id);
		}
	}
}
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
