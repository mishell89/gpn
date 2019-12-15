<template>
  <div id="app" class="page-container">
    <div class="towers-list">
      <div class="tower-item" v-for="tower in towers">
        <TowerItem :params="tower"></TowerItem>
      </div>
    </div>
    <div class="reset-data">
      <button @click="updateTowers()" class="button">Восстановить исходные значения</button>
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
          towers:[],
          btn: false
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
  methods: {
    updateTowers(){
      axios
        .get(apiURL)
        .then(res => (
          this.towers = JSON.parse(JSON.stringify(res.data))
        ));
    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Roboto&display=swap');
  body{background-color: #2d2d32;color: #ffffff;margin: 0; -webkit-font-smoothing: antialiased;font-family: 'Roboto', sans-serif;}
  .page-container{padding: 40px 50px;max-width: 1500px;margin: 0 auto;}
  .towers-list{
    display: flex;
    align-content: flex-start;
    justify-content: center;
    flex-wrap: wrap;
    margin: 0 -15px;
  }
  .reset-data{
    text-align: center;
    margin: 30px 0;
  }
  .button{
    cursor: pointer;
    background: none;
    color: #ffffff;
    border: 2px solid #ffffff;
    line-height: 40px;
    border-radius: 20px;
    white-space: nowrap;
    padding: 0 25px;
    box-shadow: none;
    display: inline-block;
    outline: none;
    transition: color .2s ease-out, border-color .2s ease-out, background-color .2s ease-out;
  }
  .button:hover,.button:active{color: #ffffff;background-color: #21b249;border-color: #21b249;}
  .button:disabled{pointer-events: none;opacity: .3;}
  @media (max-width: 510px) {
    .page-container{padding: 30px 20px;}
  }

</style>
