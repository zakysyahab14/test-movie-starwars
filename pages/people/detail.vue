<template>
    <div class="container detail">
        <h1>
            {{ peopleDetail.name }}
        </h1>
        <div>
            Gender
            <p>{{ peopleDetail.gender }}</p>
        </div>
        <div>
            Birth Year
            <p>{{ peopleDetail.birth_year }}</p>
        </div>
        <div>
            Height / weight
            <p>{{ peopleDetail.height }} cm / {{ peopleDetail.weight }} kg</p>
        </div>
        <div>
            Hair / Skin / Eye Color
            <p>{{ peopleDetail.hair_color }} / {{ peopleDetail.skin_color }} / {{ peopleDetail.eye_color }} </p>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            peopleId: null,
            peopleDetail: {}
        }
    },
    mounted() {
        this.getDetail(this.$route.query.params)
    },
    methods: {
    async getDetail(v) {
        let searchUrl = v
        await this.$axios.$get(searchUrl).then((result) => {
        this.peopleDetail = result
         }).catch((err) => {
        console.log(err)
      });

    },
    }
}
</script>