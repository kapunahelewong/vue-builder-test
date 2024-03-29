<script>
import { fetchOneEntry, Content, isPreviewing } from '@builder.io/sdk-vue'

export default {
  data: () => ({
    canShowContent: false,
    content: null,
    apiKey: 'fe07520489dd4741b861fe3c2e19b071'
  }),
  mounted() {
    fetchOneEntry({
      model: 'page',
      apiKey: 'fe07520489dd4741b861fe3c2e19b071', // <-- Replace with your Public API Key
      userAttributes: {
        urlPath: window.location.pathname
      }
    }).then((res) => {
      this.content = res
      this.canShowContent = this.content || isPreviewing()
    })
  }
}
</script>
<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
  <div>
    <title v-if="content && content.data && content.data.title">{{ content.data.title }}</title>
    <meta
      name="description"
      v-if="content && content.data && content.data.description"
      :content="content.data.description"
    />
    <div>Below is Builder Content:</div>
    <div v-if="canShowContent">
      <div>
        Page title:
        {{ content && content.data && content.data.title }}
      </div>
      <Content model="page" :content="content" :api-key="apiKey" />
    </div>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
