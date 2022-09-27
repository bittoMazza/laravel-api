<template>
  <div class="col-6">
    <img  class="img-fluid" :src="ValidURL(post.thumb) ? post.thumb : 'storage/' + post.thumb" alt="">
    <h3>{{ post.title }}</h3>
  </div>
</template>

<script>

export default {
    props:['post'],

    methods:{
    ValidURL(str) {
    var regex = /(?:https?):\/\/(\w+:?\w*)?(\S+)(:\d+)?(\/|\/([\w#!:.?+=&%!\-\/]))?/;
        if(!regex .test(str)) {
            return false;
        } else {
            return true;
        }
    },
    }
}

</script>

<style>

</style>