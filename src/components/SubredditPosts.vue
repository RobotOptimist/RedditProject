<template>
        <ul>
            <li v-for="post in filteredPosts" :key="post.data.id">
                <subreddit-post :post="post.data"></subreddit-post>
            </li>
        </ul>
</template>

<script>
    import SubredditPost from "./SubredditPost.vue"
    export default {
        props: {
                items: null,
            },
        data() {
            return {
                posts: this.items
            }
        },
        computed: {
            filteredPosts() {
                return this.posts.filter(p => p.data.selftext === (""))
            }
        },
        components: {
            "subreddit-post" : SubredditPost
        }
    }
</script>