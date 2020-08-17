<template>
  <div>
      <footer>
          <p>
              Made with extra 💙 by Desiré.
          </p>
      </footer>
  </div>
</template>

<script>
    export default {
        name: 'FooterCustom'
    }
</script>

<style lang="scss" scoped>

    footer {
        position: fixed;
        bottom: 0;
        left: 0;
        width: 100%;
        -webkit-user-select: none; /* Safari */
        -ms-user-select: none; /* IE 10+ and Edge */
        user-select: none; /* Standard syntax */
    }

    p {
        font-size: 0.8rem;
    }
</style>