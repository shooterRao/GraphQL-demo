<template>
  <div class="category">
    <!-- 组件形式注入 -->
    <ApolloQuery :query="require('../graphql/Category.gql')">
      <template v-slot="{ result: { loading, error, data }, isLoading }">
        <!-- Loading -->
        <div v-if="isLoading" class="loading apollo">Loading...</div>

        <!-- Error -->
        <div v-else-if="error" class="error apollo">An error occured</div>

        <!-- Result -->
        <div v-else-if="data" class="result apollo">
          <ul class="category">
            <li
              v-for="item in data.getAllCategories"
              :key="item.name"
            >
            <span>
              {{ item.name }} ({{ item.num }})
            </span></li>
          </ul>
        </div>

        <!-- No result -->
        <div v-else class="no-result apollo">No result :(</div>
      </template>
    </ApolloQuery>
  </div>
</template>

<script>
export default {
  name: "Category"
};
</script>

<style scoped>
.category {
  width: 200px;
  margin: 0 auto;
}
.category li {
  text-align: left;
  list-style: none;
  position: relative;
  margin: 0.2rem 0;
  padding: 0.1rem 0.5rem 0.1rem 1.5rem;
}

.category li::before {
  display: inline-block;
  top: 10px;
  margin-left: 0.45rem;
  width: 0.3rem;
  height: 0.3rem;
  border: 0.15rem solid #49b1f5;
  border-radius: 0.3rem;
  background: #fff;
  content: "";
  line-height: 0.3rem;
}
</style>