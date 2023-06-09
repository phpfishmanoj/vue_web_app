<template>
    <p>
        <RouterLink to="/new" class="btn btn-success">Add Post</RouterLink>
    </p>

    <div>
        Post List
        <!-- <pre>
            {{ postList }}
        </pre> -->
        <!-- <PostItem v-for="post of postList" :key="post.id" :post="post" @delete="onDelete" /> -->
        <PostItem v-for="post of postList" :key="post.id" :post="post" />
    </div>
</template>

<script setup>
import { computed, onMounted, ref } from 'vue';
import PostItem from "../components/PostItem.vue";

import { useStore } from "vuex";

const store = useStore()
const postList = computed(() => store.state.posts);
//const postList = ref([]);

// onMounted(() => {
//     fetch("https://jsonplaceholder.typicode.com/posts")
//         .then((res) => res.json())
//         .then((posts) => {
//             postList.value = posts;
//         });
// });

// function onDelete(post) {
//     postList.value = postList.value.filter((p) => p.id != post.id)
// }
</script>

<style lang="scss" scoped></style>