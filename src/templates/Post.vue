<template>
  <Layout>
    <div class="has-text-centered ">
      <h1 class="title">
        {{ $page.post.title }}
      </h1>
      <PostMeta
        class=""
        :post="$page.post"
      />
    </div>
    <!-- post content section container -->
    <div class="post ">
      <figure
        v-if="$page.post.cover_image"
        class="image is-16by9"
      >
        <g-image
          :src="$page.post.cover_image"
          alt="Cover image"
        />
      </figure>

      <p v-html="$page.post.content" />

      <footer>
        <PostTags :post="$page.post" />
      </footer>
    </div>

    <div class="post-comments">
    <!-- Add comment widgets here -->
    </div>
  </Layout>
</template>

<script>
import PostMeta from '~/components/PostMeta.vue'
import PostTags from '~/components/PostTags.vue'

export default {
    components: {
        PostMeta,
        PostTags,

    },
    metaInfo() {
        return {
            title: this.$page.post.title,
            meta: [
                {
                    name: 'description',
                    content: this.$page.post.description,
                },
            ],
        }
    },
}
</script>

<page-query>
query Post($id: ID!) {
  post: post(id: $id) {
    title
    date(format: "D. MMMM YYYY")
    timeToRead
    tags {
      id
      title
      path
    }
    description
    content
    cover_image
  }
}
</page-query>

<style lang="scss" scoped>
.tag {
  align-items: center;
    background-color: #f5f5f5;
    border-radius: 4px;
    color: #4a4a4a;
    display: inline-flex;
    font-size: .75rem;
    height: 2em;
    justify-content: center;
    line-height: 1.5;
    padding-left: .75em;
    padding-right: .75em;
    white-space: nowrap;
}
.title:not(:last-child) {
  margin-bottom: 0.5rem;
}
.title {
  font-family: 'Noto Serif KR';
  font-weight: 700;
}
</style>
