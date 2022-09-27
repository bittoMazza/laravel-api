<template>
   <div>
        <h1>
            Ciao sono un titolone
        </h1>
   </div>
</template>

<script>
import Axios from 'axios';

export default {
    name: "App",
    data:function(){
        return{
            posts : [],
        }
    },
    components:{

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