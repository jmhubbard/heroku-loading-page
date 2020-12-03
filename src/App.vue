<template>
  <h1>Please wait while the app is loading</h1>
  <div class="container">
    <div class="loader"></div>
  </div>
</template>

<script>
export default {
  mounted() {
    function getStatusCode() {
      const queryString = window.location.search;
      const urlParams = new URLSearchParams(queryString);
      const url = urlParams.get("url");

      fetch(`https://${url}`, {})
        .then((response) => {
          if (response.status >= 200 && response.status < 300) {
            window.location.href = `https://${url}`;
          } else {
            console.log(response.status);
          }
        })
        .catch((err) => {
          console.error(err.message);
        });
    }
    setInterval(getStatusCode, 3000);
  },
};
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

.container {
  display: flex;
  justify-content: center;
}

.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #3498db; /* Blue */
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
