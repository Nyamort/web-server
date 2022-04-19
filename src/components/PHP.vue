<template>
  <h3>PHP</h3>
  <div>
    <label for="version-php">PHP Version</label>
    <select id="version-php">

    </select>
  </div>
  <div>
    <div>
      <label for="new-version-php">Version</label>
      <select id="new-version-php" @change="newVersionPHPChange">
        <option>{{this.selectedVersion}}</option>
      </select>
    </div>
    <div>
      <label for="new-subversion-php">SubVersion</label>
      <select id="new-subversion-php">
        <option v-for="subversion in subversions" >{{subversion.version}}</option>
      </select>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PHP",
  data() {
    return {
      versions: {},
      subversions: {},
      selectedVersion: "",
      selectedSubversion: ""
    };
  },
  created: function() {
    axios.get('https://www.php.net/releases/index.php?json')
      .then(response => {
        this.versions = response.data;

        this.selectedVersion = Object.keys(this.versions).pop();
      })
      .catch(error => {
        console.log(error)
      })
  },
  methods:{
    newVersionPHPChange: function(event){
      this.selectedVersion = this.versions[event.target.selectedIndex];
      axios.get('https://www.php.net/releases/index.php?json&version=' + this.selectedVersion)
        .then(response => {
          let data = response.data;
          this.subversions = data[this.selectedVersion];
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>

<style scoped>

</style>