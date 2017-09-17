<template>
    <div class="container">
        <h1>James's Reddit App</h1>
        <div class="subreddit-container">
            <subreddit v-for="reddit in redditDefaults" :subreddit="reddit" :key="reddit.data.id"></subreddit>
        </div>
    </div>
</template>

<script>
    import Subreddit from "./Subreddit.vue"
    export default {
        data() {
            return {
                redditDefaults: []
            }
        },
        methods: {
            getRedditDefaults() {
                this.$http.get("https://www.reddit.com/subreddits/default.json")
                    .then(response => {
                            return response.json()
                    }).then(response => {
                        this.redditDefaults = response.data.children;
                    })
            }
        },
        components: {
            subreddit: Subreddit
        },
        mounted() {
            this.getRedditDefaults();
        }
    }
</script>

<style>

</style>
