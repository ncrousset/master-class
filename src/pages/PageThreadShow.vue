<template>
  <div class="col-large push-top">
    <h1>{{ thread.title }}</h1>
    <PostList :posts="posts"></PostList>
    <PostEditor
      :threadId="id"
      @save="addPost"
    />
  </div>
</template>

<script>
    import sourceData from '@/data'
    import PostList from '@/components/PostList'
    import PostEditor from '@/components/PostEditor'

    console.log(sourceData)
    export default {
        components: {
            PostList,
            PostEditor
        },
        props: {
            id: {
                required: true,
                type: String
            }
        },
        data() {
            return {
                thread: sourceData.threads[this.id],
                newPostTest: ''
            }
        },
        computed: {
            posts() {
                const postIds = Object.values(this.thread.posts)
                return Object.values(sourceData.posts)
                    .filter(post => postIds.includes(post['.key']))
            }
        },
        methods: {
            addPost(eventData) {
                console.log(eventData)
                const post = eventData.post
                const postId = eventData.post['.key']
                this.$set(sourceData.posts, postId, post)
                this.$set(this.thread.posts, postId, postId)
                this.$set(sourceData.users[post.userId].posts, postId, postId)
                //
                // this.newPostTest = ''
            }
        }
    }
</script>

<style scoped>

</style>
