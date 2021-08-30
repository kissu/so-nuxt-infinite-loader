<template>
  <div class="small-height">
    <div v-for="user in users" :key="user.id">
      <p class="user">
        <span>{{ user.first_fame }}</span>
        <span>{{ user.last_name }}</span>
        <br />
        <span>{{ user.email }}</span>
        <br />
        <img :src="user.avatar" />
      </p>
    </div>

    <infinite-loading
      ref="infiniteLoader"
      @infinite="infiniteHandler"
    ></infinite-loading>
  </div>
</template>

<script>
import InfiniteLoading from 'vue-infinite-loading'

export default {
  name: 'Child',
  components: {
    InfiniteLoading,
  },
  props: {
    users: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      page: 1,
    }
  },
  methods: {
    infiniteHandler($state) {
      this.page += 1
      this.$emit('fetchMore', this.page)
    },
  },
}
</script>

<style scoped>
.small-height {
  height: 200px;
  border: 2px solid red;
  width: 400px;
  overflow-y: auto;
}
.user {
  height: 200px;
}
</style>
