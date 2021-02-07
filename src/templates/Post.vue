<template>
  <Layout>
    <!-- Page Header -->
    <header class="masthead" :style="{
      backgroundImage:`url(http://localhost:1337${$page.strapiPost.cover.url})`
    }">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{$page.strapiPost.titile}}</h1>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Post Content -->
    <article>
      <div class="container">
        <div class="row">
          <div v-html="mdToHtml($page.strapiPost.content)">

          </div>
         
        </div>
      </div>
    </article>
  </Layout>
</template>
<page-query>

query ($id:ID!){
  strapiPost (id:$id){
    id,
    titile,
    content,
    cover{
      url
    }
  }
}
</page-query>

<script>
import MarkdownIt from 'markdown-it'
const md = new MarkdownIt()

export default {
  name: "PostPage",
  methods:{
    mdToHtml(markdown){
      return md.render(markdown)
    }
  }
};
</script>

<style></style>
