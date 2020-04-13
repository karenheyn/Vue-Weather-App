<template>
  <div id="app">
    <main>
      <form action="submit" class="search-container">
        <input type="text" class="search-bar" placeholder="Search..." />
      </form>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "56d8665da94e425b19bae655a790938a"
    };
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  background-image: url("./assets/cold-grey.jpg");
  background-size: cover;
  background-position: center;
  min-height: 400ms;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.search-container {
  width: 100%;
  margin-bottom: 30px;
}

.search-container .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background-color: rgba(255, 255, 255 0.15);
}
</style>
