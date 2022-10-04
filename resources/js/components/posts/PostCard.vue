<template>
    <div class="card mb-3">
        <img :src="post.thumb" class="card-img-top" :alt="post.title" />
        <div class="card-body">
            <h5 class="card-title">{{ post.title }}</h5>
            <p class="card-text">{{ post.content }}</p>
            <p class="card-text">
                <small class="text-muted">{{ publishedAt }}</small>
            </p>
        </div>
    </div>
</template>

<script>
export default {
    name: "PostCard",
    props: {
        post: Object,
    },
    computed: {
        publishedAt() {
            const postDate = new Date(this.post.updated_at);
            let day = postDate.getDate();
            let month = postDate.getMonth() + 1;
            let year = postDate.getFullYear();

            if (day < 10) day = "0" + day;
            if (month < 10) month = "0" + month;

            return `${day}-${month}-${year}`;
        },
    },
};
</script>
