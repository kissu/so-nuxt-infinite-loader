<template>
  <div>
    <nuxt-link :to="{ name: 'redirect' }">
      Go to another page and come back to have this one triggered
    </nuxt-link>

    <child ref="child" :users="users" @fetchMore="callApi"></child>
  </div>
</template>

<script>
export default {
  name: 'ParentPage',
  async asyncData({ $axios }) {
    const { data } = await $axios.$get(
      'https://reqres.in/api/users?per_page=2&page=1'
    )
    return { users: data }
  },
  methods: {
    async callApi(newPageAsked) {
      const { data: newUsers } = await this.$axios.$get(
        `https://reqres.in/api/users?per_page=2&page=${newPageAsked}`
      )
      console.log('new users fetched? ', newUsers)

      if (newUsers.length) {
        // if API got some new users, add them to the current list
        this.users = [...this.users, ...newUsers]
        // tell `infinite-loading` component that the fetch was successful
        this.$refs.child.$refs.infiniteLoader.stateChanger.loaded()
      } else {
        // if the API do not have anymore users to fetch
        this.$refs.child.$refs.infiniteLoader.stateChanger.complete()
      }
    },
  },
}
</script>
