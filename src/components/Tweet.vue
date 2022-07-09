<script setup lang="ts">
import {
    ref,
    Ref
} from 'vue'
import tweetData from '../TweetData.json'
import TweetPostForm from './TweetPostForm.vue';
import TweetList from './TweetList.vue';

const inputtingDescription = ref < string > ('')
const tweets = ref(tweetData);

const postTweets = (description: string) => {
    const tweet = {
        id: Math.random(),
        description
    }
    tweets.value.push(tweet)
    inputtingDescription.value = ''
}

const deleteTweets = (id: number) => {
    tweets.value = tweets.value.filter(tweet => tweet.id !== id);
}
</script>

<template>
<div class="container">
    <h1>Tweeter</h1>
    <div class="form-container">
        <TweetPostForm @post-tweet="postTweets" />
    </div>
    <div class="tweet-container">
        <p v-if="tweets.length <= 0 ">No tweets have been added</p>
        <ul v-else>
            <TweetList :tweets="tweets" @delete-tweet="deleteTweets" />
         </ul>
    </div>
</div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.form-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: aliceblue;
    padding: 10px 0;
    width: 60%;
    margin-bottom: 12px;
    border-radius: 4px;
}

.save-button {
    margin-top: 15px;
    color: #fff;
    font-weight: bold;
    background-color: #68c9c9;
    border-radius: 2px;
    border: none;
    width: 60px;
    height: 22px;
}

.save-button:hover {
    background-color: #37bdbd;
}

</style>
