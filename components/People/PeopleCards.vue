<template>
  <div class="container">
    <div class="search row" @keyup.enter="search">
      <div class="input col-10">
        <input type="text" class="icon" placeholder="Find a film title" v-model="searchValue" />
      </div>
      <div class="contro col-2">
        <b-button variant="outline-primary" class="button" v-on:click="search">Search</b-button>
      </div>
    </div>
    <div class="columns">
      <div class="column" v-for="(people, index) in peoples" :key="index">
        <div class="card">
          <div class="content">
            <p>{{ people.name }}</p>
            <div>
              Gender
              <p>{{ people.gender }}</p>
            </div>
            <div>
              Birth Year
              <p>{{ people.birth_year }}</p>
            </div>
            <div>
              Height / weight
              <p>{{ people.height }} cm / {{ people.weight }} kg</p>
            </div>
            <div>
              Hair / Skin / Eye Color
              <p>{{ people.hair_color }} / {{ people.skin_color }} / {{ people.eye_color }} </p>
            </div>
          </div>
          <div>
            <b-button variant="outline-primary" :href="`/people/detail?params=${people.url}`">See Details</b-button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    // peoples: {
    //   type: Array,
    //   default: []
    // }
  },
  data() {
    return {
      peoplesUrl: 'https://swapi.dev/api/people',
      peoples: [],
      searchValue: null,
    }
  },
  mounted() {
    this.getFilms()
  },
  methods: {
    async getFilms(v) {
      if (v === 'isSearch') {
        let searchUrl = this.peoplesUrl + '/?search=' + this.searchValue
        await this.$axios.$get(searchUrl).then((result) => {
        this.peoples = result.results
      }).catch((err) => {
        console.log(err)
      });
      }
      else {
        await this.$axios.$get(this.peoplesUrl).then((result) => {
          this.peoples = result.results
        }).catch((err) => {
          console.log(err)
        });
      }
    },
    async search() {
      this.getFilms('isSearch')
    }
  }
}
</script>

<style scoped>
  * {
    text-align: center;
  }
  .columns {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    flex-wrap: wrap;
    width: 100%;
    max-width: 1300px;
    margin: 0 auto;
    gap: 10px;
    margin-top: 50px;
  }
  .column {
    width: 24%;
    margin-bottom: 20px;
  }
  .card {
    border-radius: 15px 15px 15px 15px;
    background: #262626;
    width: 100%;
    box-sizing: border-box;
    height: 100%;
    min-height: 320px;
    margin-right: 5px;
    margin-left: 5px;
    padding-bottom: 10px;
  }
  .card:hover {
    margin-top: -20px;
    transition: .2s;
    box-shadow: 0px 0px 30px 10px #a9a9a9;
    cursor: pointer;
    background: #fff;
  }
  .card:hover .content {
    font-weight: bold;
    color: #4d4d4d;
  }
  .card:hover img {
    font-family: "Asap";
    font-weight: bold;
    font-size: 16px;
    color: #4d4d4d;
  }
  img {
    width: 100%;
    height: 300px;
    object-fit: cover;
    object-position: 50% 50%;
    border-radius: 15px 15px 0 0;

    font-family: "Asap";
    font-weight: medium;
    font-size: 16px;
    color: #fff;
    border: none;
  }
  .content {
    font-family: "Asap";
    font-weight: medium;
    font-size: 16px;
    color: #fff;
    padding: 5px;
  }
  .input input {
  width: 100%;
  margin: 0 auto 30px;
	padding: 18px 48px;
  border: 1px solid #4d4d4d;
  background:transparent;
  text-align: center;
	font-family: "Asap";
  font-weight: bold;
	font-size: 16px;
	color: #4d4d4d;
  border-radius: 15px 15px 15px 15px;
  outline: none;
  background: #fff;
}
.input input:hover {

  box-shadow: 0px 10px 15px 8px #cacaca;
}
.button {
  width: 100%;
	padding: 18px 48px;
  border-radius: 15px 15px 15px 15px;
}
.search {
  margin-top: 30px;
}
.icon {
  padding-left: 25px !important;
  background: url("https://static.thenounproject.com/png/101791-200.png") no-repeat left !important;
  background-size: 40px !important;
}
/* .button:hover {
  font-weight: bold;
  background: #fff;
  border: 1px solid #fff;
  box-shadow: 0px 10px 15px 8px #cacaca;
} */
</style>
