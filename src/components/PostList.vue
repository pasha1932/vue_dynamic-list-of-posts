<script>
import Loader from './Loader.vue'

export default {
  name: 'PostList',
  components: { Loader },
  props: {
    posts: Array,
    open: Function,
    openPost: Function,
    isLoading: Boolean,
  },
}
</script>
<template>
  <div class="tile is-parent">
    <div class="tile is-child box is-success">
      <div class="block">
        <div className="block is-flex is-justify-content-space-between">
          <p className="title">Posts</p>
          <button type="button" className="button is-link" @click="open">Add New Post</button>
        </div>
        <Loader v-if="isLoading" />

        <table
          v-if="posts.length > 0 && !isLoading"
          className="table is-fullwidth is-striped is-hoverable is-narrow"
        >
          <thead>
            <tr className="has-background-link-light">
              <th>ID</th>
              <th>Title</th>
              <th className="has-text-right">Actions</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="post of posts" :key="post.id">
              <td>{{ post.id }}</td>
              <td>{{ post.title }}</td>
              <td className="has-text-right is-vcentered">
                <button type="button" className="button is-link" @click="openPost(post)">
                  Open
                </button>
              </td>
            </tr>
          </tbody>
        </table>
        <div v-if="posts.length === 0 && !isLoading" className="block">
          <p className="title is-4">No posts yet</p>
        </div>
      </div>
    </div>
  </div>
</template>
