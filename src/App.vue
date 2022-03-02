<template>
  <div>
    <main>
      <div>
          <MainTitle/>
          <SearchBars/>
      </div>
    </main>
  </div>
</template>

<script>
import MainTitle from './components/MainTitle.vue'
import SearchBars from './components/SearchBars.vue'

export default {
  name: 'App',
  components: {
    MainTitle,
    SearchBars,
  },

}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  #app {
    background-color:aquamarine;
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }

  main {
    min-height: 100vh;
    padding: 25px;
    background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.25));
  }

</style>
