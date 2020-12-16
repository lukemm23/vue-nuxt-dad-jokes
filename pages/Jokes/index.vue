<template>

  <div>
      <SearchJokes v-on:search-text="searchText"/>
      <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke" />
  </div>
</template>

<script>
import axios from 'axios';
import Joke from '../../components/joke.vue'
import SearchJokes from '../../components/searchJokes.vue'

export default {
    components:{
        Joke,
        SearchJokes
    },
    data(){
        return {
            jokes:[]
        }
    },
    async created(){
        const config = {
            headers:{
                'Accept':'application/json'
            }
        }
        try {
            const res = await axios.get('https://icanhazdadjoke.com/search', config);
           this.jokes = res.data.results;
        } catch (err) {
            console.log('there was a error',err);
        }

    },
    methods:{
        async searchText(text){
            const config = {
            headers:{
                'Accept':'application/json'
            }
        }
        try {
            const res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config);
           this.jokes = res.data.results;
        } catch (err) {
            console.log('there was a error',err);
        }
        }
    },
    head(){
        return {
            title: 'Dad Jokes',
            meta:[
                {
                    hid:'description',
                    name:'description',
                    content:'best place for corny dad jokes',
                }
            ]
        }
    }
}
</script>

<style>

</style>