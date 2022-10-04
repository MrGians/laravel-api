<template>
    <section id="post-list" class="mt-4">
        <h2 class="text-center">Lista dei Post</h2>
        <div v-if="isLoading">
            <AppLoader />
        </div>
        <div v-else>
            <div class="row">
                <div v-if="postsList.length">
                    <div class="col-6" v-for="post in postsList" :key="post.id">
                        <!-- TODO <PostCard :post="post" /> -->
                    </div>
                </div>
                <div class="col" v-else>
                    <h4>Non è presente nessun Post</h4>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import axios from "axios";
import AppLoader from "../AppLoader";
import PostCard from "./PostCard";
export default {
    name: "PostPage",
    components: { AppLoader, PostCard },
    data() {
        return {
            api: {
                endpoint: "http://127.0.0.1:8000/api/posts",
            },
            postsList: [],
            isLoading: false,
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
                .catch((err) => {})
                .then(() => {
                    this.isLoading = false;
                });
        },
    },
    mounted() {
        this.fetchPosts();
    },
};
</script>
