<template>
  <div id="app">
    <div class="towers-list">
      <div class="tower-item" v-for="tower in towers">
        <TowerItem :params="tower"></TowerItem>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'
import TowerItem from './components/TowerItem'

const apiURL = "https://api.myjson.com/bins/1cdcjc"

export default {
  name: 'App',
  components: {
    TowerItem
  },
	data () {
		return {
          towers:[]
        }
	},
	async created() {
		try {
			const res = await axios.get(apiURL)
			this.towers = JSON.parse(JSON.stringify(res.data));
		} catch(e) {
			console.error(e)
		}
	},
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
