<template>
    <div class="container detail">
        <h1>
            {{ filmDetail.title }}
        </h1>
        <p>
            {{ filmDetail.release_date }}
        </p>
        <p>
            {{ filmDetail.director }}
        </p>
        <p>
            {{  filmDetail.producer }}
        </p>
        <div>
            <p>
                {{ filmDetail.opening_crawl }}
            </p>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            filmId: null,
            filmDetail: {}
        }
    },
    mounted() {
        this.getDetail(this.$route.query.params)
    },
    methods: {
    async getDetail(v) {
        let searchUrl = v
        await this.$axios.$get(searchUrl).then((result) => {
        this.filmDetail = result
         }).catch((err) => {
        console.log(err)
      });

    },
    }
}
</script>