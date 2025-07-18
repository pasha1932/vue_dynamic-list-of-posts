<script>
export default {
  name: 'AddPost',
  data() {
    return {
      title: '',
      body: '',
      errorTitle: false,
      errorBody: false,
    }
  },
  props: {
    close: Function,
    isCreated: Boolean,
    createPost: Function,
  },
  methods: {
    handleSubmit() {
      if (!this.title) {
        this.errorTitle = true
      }

      if (!this.body) {
        this.errorBody = true
      }

      if (this.errorTitle || this.errorBody) {
        return
      }

      this.createPost({
        userId: 2049,
        title: this.title,
        body: this.body,
      })

      this.title = ''
      this.body = ''
      this.errorTitle = false
      this.errorBody = false
    },
  },
}
</script>
<template>
  <div class="tile is-parent is-8-desktop Sidebar" :class="{ 'Sidebar--open': isCreated }">
    <div class="tile is-child box is-success">
      <div className="content">
        <div className="content">
          <h2>Create new post</h2>

          <form @submit.prevent="handleSubmit">
            <div className="field" data-cy="NameField">
              <label className="label" htmlFor="{`comment-author-name-${name}`}"> Title </label>
              <div className="control has-icons-left has-icons-right">
                <input
                  type="text"
                  name="{name}"
                  id="{`comment-author-name-${name}`}"
                  placeholder="Post title"
                  class="input"
                  :class="{ 'is-danger': errorTitle }"
                  v-model="title"
                  @input="errorTitle = false"
                />
                <span className="icon is-small is-left">
                  <i className="fas fa-user"></i>
                </span>

                <span
                  className="icon is-small is-right has-text-danger"
                  v-if="errorTitle"
                  data-cy="ErrorIcon"
                >
                  <i className="fas fa-exclamation-triangle"></i>
                </span>
              </div>

              <p className="help is-danger" v-if="errorTitle" data-cy="ErrorMessage">
                Title is required
              </p>
            </div>
            <div className="field" data-cy="BodyField">
              <label className="label" htmlFor="{`comment-${name}`}"> Write post body </label>
              <div className="control">
                <textarea
                  id="{`comment-${name}`}"
                  name="name"
                  placeholder="Post body"
                  class="textarea"
                  :class="{ 'is-danger': errorBody }"
                  v-model="body"
                  @input="errorBody = false"
                ></textarea>
              </div>

              <p className="help is-danger" v-if="errorBody" data-cy="ErrorMessage">
                Body is required
              </p>
            </div>

            <div className="field is-grouped">
              <div className="control">
                <button type="submit" className="button is-link">Create</button>
              </div>
              <div className="control">
                <button type="reset" className="button is-link is-light" @click="close">
                  Cancel
                </button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
