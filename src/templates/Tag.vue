<template>
<div>
  <h1>Tag PAGE</h1>
  <p>tag is:{{$page.strapiTag.title}}</p>
  <p  v-for="posts in $page.strapiTag.posts"
              :key="posts.id">
            <b>id:{{posts.id}}</b><br>
            <b>title:{{posts.titile}}</b>

            goto :
              <g-link :to="'/post/' + posts.id">
                <h2 class="post-title">
                  {{ posts.titile }}
                </h2>
              </g-link>

  </p>
</div>
</template>
<page-query>

query ($id:ID!){
  strapiTag (id:$id){
    id,
    title,
    posts{
      id
      titile
    }
  }
}
</page-query>


<script>

export default {
  name: "TagPage",
 
};
</script>

<style></style>
