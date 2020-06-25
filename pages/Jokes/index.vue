<template>
  <div>
      <SearchJokes v-on:search-text="searchText"/>
      <Joke v-for="joke in jokes" :key="joke.id" 
      :id="joke.id" :joke="joke.joke" />
  </div>
</template>

<script>
import Joke from '../../components/joke'
import SearchJokes from '../../components/SearchJokes'
import axios from 'axios';

export default {
    components: {
        Joke,
        SearchJokes
    },
    data(){
        return{
            jokes: []
        }
    },
    async created(){
        const config = {
            headers: {
                'Accept': 'application/json'
            }
        }
        try {
            const res = await axios.get('https://icanhazdadjoke.com/search', config);
            this.jokes = res.data.results;
        } catch (error) {
            console.log(err)
        }
    },
    methods: {
        async searchText(text){
        const config = {
            headers: {
                'Accept': 'application/json'
            }
        }
        try {
            const res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config);
            this.jokes = res.data.results;
        } catch (error) {
            console.log(err)
        }
        }
    },
    head(){
        return {
            title: 'Dad Jokes',
            meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Best place for corny dad jokes'
                }
            ]
        }
    }

}
</script>

<style>

</style>