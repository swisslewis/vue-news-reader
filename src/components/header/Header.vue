<template>
  <nav>
      <ul>
          <li><router-link v-bind:to="'/'">Home</router-link></li>
          <li><router-link v-bind:to="'/about'">About</router-link></li>
      </ul>
  </nav>
</template>

<script>
export default {
    name: "MyHeader"
}
</script>

<style scoped>

    ul {
        list-style-type: none;
        display: flex;
        justify-content: center;
        padding: 0px;
    }

    li a {
        text-decoration: none;
        padding: 10px;
        font-family: sans-serif;
        color: green;
    }

    a:hover {
        color: purple;
    }

    .router-link-exact-active {
        font-weight: bold;
        text-decoration: none;
    }
</style>