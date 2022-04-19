<template>
  <h3>PHP</h3>
  <div>
    <label for="version-php">PHP Version</label>
    <select id="version-php">

    </select>
  </div>
  <div>
    <div>
      <label for="new-version-php">New Version</label>
      <select id="new-version-php">
      </select>
    </div>
    <div>
      <label for="new-subversion-php">SubVersion</label>
      <select id="new-subversion-php">
      </select>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PHP",
  created: function() {
    axios.get('https://www.php.net/releases/index.php?json')
      .then(response => {
        console.log(response.data);
      })
      .catch(error => {
        console.log(error)
      })
  },
}
</script>

<style scoped>

</style>