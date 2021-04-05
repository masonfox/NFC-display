<template>
  <div>
    <h1>Easy copy to clipboard</h1>
    <p>Add ?value=text_you_want_to_copy</p>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      urlParams: null,
      val: '',
      success: false
    }
  },
  methods: {
    async copy () {
      await navigator.clipboard.writeText(this.val)
      this.success = true
      this.clear()
    },
    clear () {
      // remove query string
      window.history.replaceState(null, null, window.location.pathname);
      // remove local state
      this.val = ''
    }
  },
  created () {
    this.urlParams = new URLSearchParams(window.location.search)

    if (this.urlParams.has('value')) {
      this.val = this.urlParams.get('value')
      this.copy()
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
