<template>

<div class="container">
    <PostCard v-for="post in posts" :key="post.id" :post="post"/>
</div>

</template>

<script>
import Axios from 'axios';
import PostCard from '../components/PostCard';
export default {
    name: "App",
    data:function(){
        return{
            posts : [],
        }
    },
    components:{
        PostCard,
    },
    methods:{
        getPosts(postsPage = 1){
            Axios.get('/api/posts',{
                page: postsPage
            }).then((response) => {
                console.log(response.data.results);
                this.posts = response.data.results.data;
            }).catch((error) => {
                console.error(error);
            })
        }
    },
    created(){
        this.getPosts();
    }


}
</script>

<style>

</style>