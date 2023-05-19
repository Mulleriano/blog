<script>
import PostForm from '../components/PostForm.vue';

export default {
  components: {
    PostForm,
  },
  props: {
    posts: Array,
  },
  data() {
    const id = this.$route.params.id;
    
    return {
      id: id,
      post: this.posts[id],
    };
  },
};
</script>

<template>
  <PostForm :post="post" :id="id"/>
</template>
