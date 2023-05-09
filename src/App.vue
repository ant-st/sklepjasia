<script setup>
import TheStore from "@/components/TheStore.vue";

</script>

<template>
  <header>
    <h1>Domki z lasu</h1>
    <img src="./assets/logo.png" alt="shop logo"/>
  </header>
  <main>
    <TheStore />
  </main>
</template>

<style scoped>


header {
  line-height: 1.5;
  grid-area: banner;
  display: flex;
  flex-direction: column;
  height: 100%;
  justify-content: center;
  overflow: hidden;
}

header h1 {
  font-family: Amatic SC, serif;
  font-size: max(50px,min(80px,7vw));
  color: #407700;
  width: 100%;
  text-align: center;
  margin: 30px auto;
}

header img {
  height: auto;
  width: 90%;
  margin: 10px auto;
}

main {
  height: 100%;
  grid-area: store;
  display: grid;
  grid-template-columns: 1fr 350px;
  grid-template-areas: 'store settings';
}

@media screen and (max-width: 1000px) {
  main {
    grid-template-columns: 1fr 1fr;
  }
  @media screen and (max-width: 650px) {
    header {
      display: inline-flex;
      flex-direction: row;
      height: 100%;
    }
    header h1 {
      margin: 0;
      width: 60%;
      padding: 20px 0;
    }
    header img {
      height: 100px;
      width: 100px;
      margin: 10px;
    }
    main {
      grid-template-columns: 1fr;
      grid-template-rows: auto;
      grid-template-areas: 'settings' 'store';
    }
  }
}



</style>
