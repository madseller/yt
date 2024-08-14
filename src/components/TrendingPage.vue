<template>
    <h1 v-t="'titles.trending'" class="text-center font-bold" />
    <LoadingIndicatorPage :show-content="videos.length != 0" class="video-grid">
        <VideoItem v-for="video in videos" :key="video.url" :item="video" height="118" width="210" />
    </LoadingIndicatorPage>
</template>

<script>
import LoadingIndicatorPage from "./LoadingIndicatorPage.vue";
import VideoItem from "./VideoItem.vue";

export default {
    components: {
        VideoItem,
        LoadingIndicatorPage,
    },
    data() {
        return {
            videos: [],
        };
    },
    mounted() {
        if (
            this.$route.path == import.meta.env.BASE_URL &&
            this.getPreferenceString("homepage", "trending") == "feed"
        ) {
            return;
        }
        let region = this.getPreferenceString("region", "RU");
        //console.log(region)
        this.fetchTrending(region).then(videos => {
            this.videos = videos;
            this.updateWatched(this.videos);
            this.fetchDeArrowContent(this.videos);
        });
    },
    activated() {
        document.title = this.$t("titles.trending") + " - Fruyt ▶ Youtube";
        if (this.videos.length > 0) this.updateWatched(this.videos);
        if (this.$route.path == import.meta.env.BASE_URL) {
            let homepage = this.getHomePage(this);
            if (homepage !== undefined) this.$router.push(homepage);
        }
    },
    methods: {
        async fetchTrending(region) {
            return await this.fetchJson(this.apiUrl() + "/trending", {
                region: region || "RU",
            });
        },
    },
};
</script>
