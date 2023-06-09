<template>
    <div class="card mb-4">
        <div class="card-body">
            <h1 class="card-title">
                {{ post.title }}
            </h1>
            <p class="card-text">
                {{ post.body }}
            </p>
            <div class="text-end">
                <RouterLink :to="`/edit/${post.id}`" class="btn btn-primary me-3">Edit</RouterLink>
            </div>
            <div class="text-end">
                <button @click="onDeletePost(post)" class="btn btn-danger">Delete</button>
            </div>
        </div>
    </div>
</template>

<script setup>

import { useStore } from 'vuex';

const props = defineProps({
    post: {
        type: Object,
        required: true,
    },
});

const store = useStore();
const emit = defineEmits(['delete']);

function onDeletePost(post) {
    if (!window.confirm("Are you want to delete post?")) {
        return;
    }

    // fetch(`https://jsonplaceholder.typicode.com/posts/${post.id}`, {
    //     method: "DELETE"
    // })
    //     .then((res) => {
    //         if (res.status == 200) {
    //             emit('delete', post);
    //         }
    //     });

    store.dispatch('deletePost', post.id);
}
</script>

<style></style>