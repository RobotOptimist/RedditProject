<template>
    <div class="row post-container">
        <div class="subreddit-post">
            <div class="col-md-6">
                <a class="post-title" :href="post.url">Title: {{ post.title }}</a>
            </div>
            <div class="col-md-6">
                <img  class="col-md-3 post-thumbnail" :src="post.thumbnail"/>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ["post"],
        data() {
            return {

            }
        }
    }
</script>

<style>
    .post-title {
        color: black;
        text-align: left;
        text-transform: uppercase;  
        font-size: 10px;
        margin-top: 5px;
        margin-bottom: 5px;
    }
    .post-thumbnail {
        width:140px;
        height:140px;
        object-fit: contain;
    }
    .post-container {
        border: thin solid black;
        background-color: white;
    }
</style>