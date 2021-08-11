<template>
	<div class="main d-flex justify-content-center">
		<div class="content d-flex flex-column align-items-center">
			
			<img src="./assets/bitcoin.jpg" width="180">
			
			<div class="texts mt-4 d-flex flex-column align-items-center">
				<p class="mb-0">Bitcoin USD (BTC-USD)</p>
				<small class="text-muted" >CCC - CoinMarketCap. Currency in USD</small>
				<div v-if="isReady" class="d-flex flex-column align-items-center">
					<h1 class="my-3">{{value}} USD</h1>
					<small class="text-muted">Updated at {{updateAt}}</small>
				</div>
			</div>
			
		</div>

	</div>
</template>

<style scoped>

@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600&display=swap");
*{
	font-family: "Poppins";
}
p{
	font-size: 20px;
}
.content{
	margin-top: 5%;
}
</style>

<script>
import axios from "axios";

export default {
	data() {
		return {
			isReady: false,
			value: String,
			updateAt: String,
		};
	},
	created: async function() {
		const {data} = await axios.get("https://api.coindesk.com/v1/bpi/currentprice.json");
		this.value = data.bpi.USD.rate;
		this.updateAt = data.time.updated;
		this.isReady = true;
	},
};
</script>
