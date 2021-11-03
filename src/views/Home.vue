<template>
  <div class="home">
    <div class="feature-card">
      <router-link to='/movie/tt0409591'>
        <img 
          src="https://wallpapers.com/images/high/naruto-shippuden-nine-tails-chakra-form-3jl2ggg82jqu0aqc.jpg" 
          alt="Naruto" 
          class="featured-img"
        >
        <div class="detail">
          <h3>Naruto</h3>
          <p>Naruto Uzumaki, is a loud, hyperactive, adolescent ninja who constantly searches for approval and recognition, as well as to become Hokage, who is acknowledged as the leader and strongest of all ninja in the village.</p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent='searchMovies()' class="search-box">
      <input type="text" placeholder="What are you looking for?" v-model='search'>
      <input type="submit" value="Search">
    </form>


    <div class="movies-list">MOVIES</div>
  </div>
</template>

<script>
import {ref} from 'vue'
import env from '@/env.js'

export default {
  setup() {
    const search = ref('')
    const movies = [];

    const searchMovies = () => {
      if(search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
        .then(response => response.json())
        .then(data)
  
      }
    }
 

    return {
      search,
      movies,
      searchMovies
    };
  }
  
  
}
</script>

<style lang='scss'>
  .home {
    .feature-card {
      position: relative;

      .featured-img {
        display: block;
        width: 100%;
        height: 300px;
        object-fit: cover;

        position: relative;
        z-index: 0;
      }

      .detail {
        position: absolute;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: rgba(0, 0, 0, 0.6);
        padding: 16px;
        z-index: 1;

        h3 {
          color: #fff;
          margin-bottom: 16px;
        }

        p {
          color: #fff;
        }
      }
    }

    .search-box {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 16px;

      input {
        display: block;
        appearance: none;
        border: none;
        background: none;
        outline: none;

        &[type="text"] {
          width: 100%;
          color: #fff;
          background-color: #496583;
          font-size: 20px;
          padding: 10px 16px;
          border-radius: 8px;
          margin-bottom: 15px;
          transition: 0.4s;


          &::placeholder {
            color: #f3f3f3;
          }

          &:focus {
            box-shadow: rgba(0, 0, 0, 0.2);
          }
        }

        &[type="submit"] {
          width: 100%;
          max-width: 300px;
          background-color: #42b883;
          padding: 16px;
          border-radius: 8px;
          color: #fff;
          font-size: 20px;
          text-transform: uppercase;
          transition: 0.4s;

          &:active {
            background-color: #3b8070;
          }
        }

      }
    }
  }
</style>
