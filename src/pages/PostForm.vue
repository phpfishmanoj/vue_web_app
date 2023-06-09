<template>
    <div>
        <RouterLink to="/" class="btn btn-outline-secondary">Back</RouterLink>
        <!-- <pre>
             {{ model }}
        </pre> -->
        <form @submit.prevent="onSubmit">
            <h1>
                {{ model.id ? "Edit Post" : "Create new Post" }}
            </h1>
            <div class="mb-3">
                <input v-model="model.title" type="text" class="form-control" placeholder="Post Title" />
                <textarea v-model="model.body" class="form-control" placeholder="Post Body"></textarea>
                <p>
                    <button :disabled="!model.title || !model.body" class="btn btn-success" type="submit">
                        Submit
                    </button>
                </p>
            </div>
        </form>
    </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";
//import store from "../store";

import { useStore } from "vuex";

const store = useStore();
const route = useRoute();
const router = useRouter();

const model = ref({
    id: "",
    title: "",
    body: "",
});

onMounted(async () => {
    if (!route.params.id) {
        return;
    }
    // fetch("https://jsonplaceholder.typicode.com/posts/" + route.params.id)
    //     .then((res) => res.json())
    //     .then((post) => {
    //         model.value = post;
    //     });
    model.value = await store.dispatch('getSinglePost', route.params.id);
});

function onSubmit() {
    // if (model.value.id) {
    //     fetch("https://jsonplaceholder.typicode.com/posts/" + model.value.id, {
    //         method: "PUT",
    //         body: JSON.stringify(model.value),
    //     })
    //         .then((res) => res.json())
    //         .then((res) => {
    //             router.push("/")
    //         });
    // } else {
    //     fetch("https://jsonplaceholder.typicode.com/posts/", {
    //         method: "PUT",
    //         body: JSON.stringify(model.value),
    //     })
    //         .then((res) => res.json())
    //         .then((res) => {
    //             router.push("/")
    //         });

    // }
    store.dispatch('savePost', model.value)
        .then(() => {
            router.push('/')
        })
}

</script>

<style lang="scss" scoped></style>