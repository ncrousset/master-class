<template>
  <div class="post">
    <div class="user-info">
      <a href="#" class="user-name">{{user.name}}</a>
      <a href="#">
        <img class="avatar-large" :src="user.avatar" alt="">
      </a>
      <p class="desktop-only text-small">{{userPostCount}} posts</p>
    </div>
    <div class="post-content">
      <div>
        {{ post.text }}
      </div>
    </div>
    <AppDate :timestamp="post.publishedAt"/>
  </div>
</template>

<script>
    import sourceData from '@/data'
    export default {
        props: {
            post: {
                required: true,
                type: Object
            }
        },
        computed: {
            user() {
                return sourceData.users[this.post.userId]
            },
            userPostCount() {
                return Object.keys(this.user.posts).length
            }
        }
    }
</script>

<style scoped>

</style>
