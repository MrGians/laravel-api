<template>
    <div class="content">
        <AppHeader :title="title" />
        <main class="container">
            <PostsPage />
        </main>
    </div>
</template>

<script>
import AppHeader from "./AppHeader";
import PostsPage from "./posts/PostsPage";
export default {
    name: "App",
    components: { AppHeader, PostsPage, PostsPage },
    data() {
        return {
            title: "Boolpress",
        };
    },
};
</script>
