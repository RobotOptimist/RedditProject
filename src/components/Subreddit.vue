<template>
    <div class="col-md-4">
        <div class="reddit-card row">
            <div class="reddit-cell">
                <span class="label label-default col-md-6 reddit-label">Name:</span> 
                <input class="col-md-6 reddit-value" :value="subreddit.data.display_name" disabled/>
            </div>
            <div class="reddit-cell">
                <span class="label label-default col-md-6 reddit-label">Advertiser Category:</span> 
                <input class="col-md-6 reddit-value" :value="subreddit.data.advertiser_category ? subreddit.data.advertiser_category : 'not specified'" disabled/>
            </div>
            <div class="reddit-cell">
                <span class="label label-default col-md-6 reddit-label">Subscribers:</span> 
                <input class="col-md-6 reddit-value" :value="subreddit.data.subscribers" disabled/>
            </div>
        </div>
        <div @click="triggerPosts" v-if="!showPosts" class="reddit-post-trigger">
            <span>Click to See Posts</span>
        </div>
        <div v-if="showPosts">
            <div class="close-posts" @click="showPosts = false">Click to Close</div>
            <subreddit-posts class="subreddit-posts" :items="posts"></subreddit-posts>
        </div>
    </div>
</template>

<script>
    import Posts from "./SubredditPosts.vue"
    export default {
        props: ["subreddit"],
        data() {
            return {
                posts: [],
                showPosts: false
            }
        },
        methods: {
            getSubRedditPosts() {
                let url = "https://www.reddit.com";
                url = url + this.subreddit.data.url + "hot.json"
                this.$http.get(url)
                    .then(response => {
                        return response.json();
                    })
                    .then(response => {
                        this.posts = response.data.children;
                    })
            },
            triggerPosts() {
                this.getSubRedditPosts();
                this.showPosts = true;
            }
        },
        components: {
            "subreddit-posts": Posts
        }
    }
</script>

<style>
    .reddit-card {
        display: block;
        border: thin solid black;
        background-color: #cee3f8;
        margin-top: 10px;
    }
    .reddit-label {
        position:relative;
        top:5px;
    }
    .reddit-value {
        text-align: right;
    }
    .reddit-post-trigger {
        background-color: palegoldenrod;
        font-size: 10px;
        line-height: 1;
        margin-bottom: 10px;
        text-transform: uppercase;
        cursor: pointer;
    }
    .subreddit-posts {
        position: absolute;
        z-index: 1;
        background-color: white;
        border: thin solid black;        
    }
    .close-posts {
        font-size: 10px;
        line-height: 1;
        background-color: palegoldenrod;
        text-transform: uppercase;
        cursor: pointer;
        }
</style>