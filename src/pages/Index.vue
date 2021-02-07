<template>
  <Layout>
    <div>
      <!-- Page Header -->
      <header
        class="masthead"
        :style="{
          backgroundImage: `url(http://1337${
            $page.general.edges[0].node.cover.url
          })`,
        }"
      >
        >
        <div class="overlay"></div>
        <div class="container">
          <div class="row">
            <div class="col-lg-8 col-md-10 mx-auto">
              <div class="site-heading">
                <h1>{{ $page.general.edges[0].node.title }}</h1>
                <span class="subheading">{{
                  $page.general.edges[0].node.subtitle
                }}</span>
              </div>
            </div>
          </div>
        </div>
      </header>

      <!-- Main Content -->
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div
              class="post-preview"
              v-for="edge in $page.posts.edges"
              :key="edge.node.id"
            >
              <g-link :to="'/post/' + edge.node.id">
                <h2 class="post-title">
                  {{ edge.node.titile }}
                </h2>
              </g-link>
              <p class="post-meta">
                Posted on
                {{ edge.node.created_at }}
              </p>
              <p>
                <span href="" v-for="tags in edge.node.tags" :key="tags.id">
                  <g-link :to="'/tag/' + tags.id">
                    {{ tags.title }}
                  </g-link>
                  &nbsp;</span
                >
              </p>
            </div>
          </div>
          <Pager :info="$page.posts.pageInfo" />
        </div>
      </div>
    </div>
  </Layout>
</template>
<page-query>
query($page: Int){
  posts:
  allStrapiPost(perPage:2,page:$page) @paginate{
    pageInfo{
      totalPages
      currentPage
    }
    edges {
      node {
        id
        titile
        created_at
        tags {
          id
          title
          created_at
        }
      }
    }
  }
 general: allStrapiGeneral{
    edges{
      node{
        id
        title
        subtitle
        cover{
          url
        }
      }
    }
  }
}
</page-query>

<script>
import { Pager } from "gridsome";
export default {
  name: "HomePage",
  metaInfo: {
    title: "Hello, world!",
  },
  components: {
    Pager,
  },
};
</script>

<style></style>
