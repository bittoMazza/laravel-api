<template>

<div class="container">
    <h3 class="text-center py-4"> Tutti i post </h3>
    <div class="d-flex justify-content-center flex-wrap">
        <PostCard v-for="post in posts" :key="post.id" :post="post"/>
    </div>

    <div class="py-5">
            <h2 class="text-center py-4">Titoli dei post per ogni tag</h2>
            <div class="d-flex flex-wrap justify-content-center"> 
                <div v-for="tag in tags" :key="tag.id" class="col-4">
                    <h3>{{ tag.name }}</h3>
                    <ul>
                        <li v-for="post  in tag.posts" :key="post.id">
                            {{ post.title }}
                        </li>
                    </ul>
                </div>
            </div>
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
            tags : [],
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
        },
        getTags(){
            Axios.get('/api/tags',{
            }).then((response) => {
                this.tags = response.data.results.data;
            }).catch((error) => {
                console.error(error);
            })
        }
    },
    created(){
        this.getPosts();
        this.getTags();
    }


}
</script>

<style>

</style>