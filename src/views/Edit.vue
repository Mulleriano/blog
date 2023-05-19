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
    return {
      post: this.posts[this.$route.params.id],
    };
  },
};
</script>

<template>
  <PostForm :post="post" />
</template>
