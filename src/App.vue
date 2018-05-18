<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <!-- <VideoList v-bind:videoRes="videos"></VideoList> -->
        <div class="row">
            <VideoDetail :video="selectedVideo" />
            <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

const API_KEY = 'AIzaSyBI-uuZ4BPHjfToKEBUJqjVIl14SS8pdxU';

export default {
    name: 'App',
    components: {
        SearchBar,
        VideoList,
        VideoDetail
    },
    data: () => ({
        videos: [],
        selectedVideo: null
    }),
    methods: {
        onTermChange(searchTerm) {
            axios.get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    key: API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: searchTerm
                }
            }).then(response => {
                this.videos = response.data.items;
            });
        },
        onVideoSelect(video) {
            this.selectedVideo = video;
        }
    }
};
</script>
