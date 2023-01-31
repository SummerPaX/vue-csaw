<script setup lang="ts">
import { ref } from "vue";
import BlogPost from "./BlogPost.vue";
import { BlogPostInterface } from "../interfaces/BlogPost.interface";

const blogs = ref<BlogPostInterface[]>([
	{
		id: 234,
		title: "First Blog",
		body: "So cool",
	},
	{
		id: 232,
		title: "Second Blog",
		body: "Mit Typescript ✌",
	},
]);
</script>

<template>
	<BlogPost
		v-for="blog in blogs"
		:title="blog.title"
		:body="blog.body"
		:class="{ 'bg-pink-200': blog.favourite }"
		@favouriteBlog="blog.favourite = true"
	></BlogPost>
</template>
