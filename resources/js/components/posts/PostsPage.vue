<template>
    <section id="post-list" class="mt-4">
        <h2 class="text-center mb-4">Lista dei Post</h2>
        <AppLoader v-if="isLoading" />
        <div v-else-if="error">
            <AppError :error="error" />
        </div>
        <div v-else>
            <div v-if="postsList && postsList.length">
                <div class="row">
                    <div class="col-6" v-for="post in postsList" :key="post.id">
                        <PostCard :post="post" />
                    </div>
                </div>
            </div>
            <h4 class="text-center my-3" v-else>Non è presente nessun Post</h4>
        </div>
    </section>
</template>

<script>
import axios from "axios";
import AppLoader from "./../AppLoader.vue";
import AppError from "./../AppError.vue";
import PostCard from "./PostCard.vue";
export default {
    name: "PostPage",
    components: { AppLoader, PostCard, AppError },
    data() {
        return {
            api: {
                endpoint: "http://127.0.0.1:8000/api/posts",
            },
            postsList: [],
            isLoading: false,
            error: null,
        };
    },
    methods: {
        fetchPosts() {
            this.isLoading = true;

            axios
                .get(`${this.api.endpoint}`)
                .then((res) => {
                    this.postsList = res.data.data;
                })
                .catch((err) => {
                    this.error = "Fetch Posts Error";
                })
                .then(() => {
                    this.isLoading = false;
                    console.log("Chiamata terminata");
                });
        },
    },
    mounted() {
        this.fetchPosts();
    },
};
</script>
