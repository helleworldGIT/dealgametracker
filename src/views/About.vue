<template>
  <div>
    <vue-headful
        title="Sale game garden | About"
        description="Sale game garden | A side-project. You can search best and cheap game deals here."
    />
    <div>
      <h1>
        What is this about? 🤔
      </h1>
      <p>
        Hello, internet! 👋
      </p>
      <p>
        This is a <b>side-project</b> created by <a href="https://twitter.com/helleworld_" target="_blank">Desiré</a>
      </p>
      <ul>
        <li>
          👉Tools used:👈
        </li>
        <li>
          Vue.js framework ✨
        </li>
        <li>
          Vue-Headful ✨
        </li>
        <li>
          CheapShark API ✨
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'About'
  }
</script>

<style lang="scss" scoped>
* {
  text-align: center;
  color: #00b7c2;
}

ul {
  list-style: none;
  padding-inline-start: 0;
  li {
    padding: 0.7rem;
  }
}

</style>