<template>

<div class="container">
    <h3 class="text-center py-4"> Tutti i post </h3>
    <div class="d-flex justify-content-center flex-wrap">
        <PostCard v-for="post in posts" :key="post.id" :post="post"/>
    </div>
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