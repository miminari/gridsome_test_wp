<template>
  <Layout>
    <h1>あおぞらふかく</h1>
    <ul>
      <li v-for="{ node } in $page.allWordPressPost.edges" :key="node._id">
        <router-link :to="node.path"><g-image v-if="node.featuredMedia" :src="node.featuredMedia.url.src" width="200" /></router-link>
        <div class="date" v-html="node.date"/>
        <h2><router-link :to="node.path" v-html="node.title"/></h2>
        <div v-html="node.fields.excerpt"/>
      </li>
    </ul>
    <Pager :info="$page.allWordPressPost.pageInfo"/>
  </Layout>
</template>

<page-query>
query Home ($page: Int) {
  allWordPressPost (perPage: 10, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        _id
        title
        date (format: "YYYY年MM月DD日 HH:mm:ss")
        path
        fields {
          excerpt
        }
        featuredMedia {
          url
        }
      }
    }
  }
}
</page-query>

<script>
import { Pager } from 'gridsome'

export default {
  components: {
    Pager
  }
}
</script>
