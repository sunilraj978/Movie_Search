<template>
  <div class="home">
    <div class="feature">
      <router-link style="text-decoration: none;" to="/movie/tt0409591">
        <img
          src="https://images-na.ssl-images-amazon.com/images/I/912Ip2nA1uL._RI_.jpg"
          alt=""
        />
        <div id="details">
          <h2>One Punch Man</h2>
          <p>
            One-Punch Man (Japanese: ワンパンマン, Hepburn: Wanpanman) is a
            Japanese superhero franchise created by the artist ONE. It tells the
            story of Saitama, a superhero who can defeat any opponent with a
            single punch but seeks to find a worthy opponent after growing bored
            by a lack of challenge due to his overwhelming strength.
          </p>
        </div>
      </router-link>
    </div>
  </div>
  <form @submit.prevent="searchMovies()">
    <div class="inputs">
      <input
        type="text"
        placeholder="what are searching for?"
        v-model="search"
      />
      <input class="k" type="submit" />
    </div>
  </form>
  <div class="movie-list">
    <div class="movie" v-for="movie in searchArr" :key="movie.imdbID">
      <router-link :to="'/movie' + movie.imdbID">
        <div>
          <img :src="movie.Poster" alt="" />
        </div>
        <div style="width:220px">
          <div style="display:flex;justify-content:space-between">
            <h4
              style="color:white;font-size:18px;background-color:green;width:70px;padding:3px"
            >
              {{ movie.Type }}
            </h4>
            <h4
              style="color:white;font-size:18px;background-color:grey;width:70px;padding:3px"
            >
              {{ movie.Year }}
            </h4>
          </div>
          <h2 style="color:white">{{ movie.Title }}</h2>
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import env from "@/env.js";
export default {
  setup() {
    const search = ref("");
    const searchArr = ref([]);
    const searchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apiKey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            searchArr.value = data.Search;
            search.value = "";
            console.log(searchArr.value);
          });
      }
    };
    return {
      search,
      searchArr,
      searchMovies,
    };
  },
};
</script>

<style lang="scss">
.home {
  position: relative;
  .feature img {
    display: block;
    width: 100%;
    height: 300px;
    position: relative;
    object-fit: cover;
  }
  #details {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    padding: 10px;
    z-index: 1;
    background-color: rgba(0, 0, 0, 0.6);
  }
  p {
    color: white;
  }
}
.inputs {
  display: flex;
  flex-direction: column;
  align-items: center;
}
input[type="text"] {
  width: 50%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 2px solid black;
  color: white;
  border-radius: 4px;
  background-color: #73a5c6;
}
::placeholder {
  color: white;
  font-size: 17px;
  opacity: 10; /* Firefox */
}
input[type="submit"] {
  width: 40%;
  padding: 10px;
  border: none;
  outline: 0px;
  background-color: #00ff00;
  color: black;
  border-radius: 20px;
  font-weight: bold;
}

.movie-list {
  display: flex;
  flex-wrap: wrap;
  padding: 20px;
  margin-left: 20px;
}
.movie {
  padding: 30px;
}
img {
  object-fit: cover;
  width: 70%;
}
router-link {
  text-decoration: none;
}
router-link a {
  text-decoration: none;
}
router-link a {
  text-decoration: none !important;
}
</style>
