<template>
  <v-card class="card mb-5">
    <nuxt-link
      :to="{ name: 'blog-slug', params: {
        sys: id
      }}"
      class="wrapper"
    >
      <v-card-title>{{ title }}</v-card-title>
    <v-card-text>
      <v-row
        align="center"
        class="mx-0"
      >
      </v-row>
      <div>{{ date }}</div>
    </v-card-text>
    </nuxt-link>
  </v-card>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: ''
    },
    id: {
      type: String,
      default: ''
    },
    date: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss" scoped>
.wrapper {
  text-decoration: none;
}
</style>