<template>
  <div class="content">
    <ApolloQuery :query="require('../graphql/ArticleContent.gql')" :variables="{ id }">
      <template v-slot="{ result: { data } }">
        <template v-if="data">
          <div v-html="data.getArticleContent.html"></div>
        </template>
      </template>
    </ApolloQuery>
  </div>
</template>

<script>
export default {
  name: "Content",
  computed: {
    id() {
      return this.$route.params.id ? +this.$route.params.id : 1;
    }
  }
};
</script>

<style>
</style>