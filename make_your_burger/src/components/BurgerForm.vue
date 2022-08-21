<template>
	<div>
		<Message :msg="msg" v-if="msg" />
		<div>
			<form id="burger-form" @submit="createOrder">
				<div class="input-container">
					<label for="clientName">Name:</label>
					<input type="text" name="clientName" id="clientName" required v-model="clientName" placeholder="Enter your name">
				</div>

				<div class="input-container">
					<label for="bread">Bread type:</label>
					<select name="bread" id="bread" required v-model="bread">
						<option value="" selected disabled>Choose your bread type:</option>

						<option v-for="bread in breads" :key="bread.id" :value="bread.name">
							{{ bread.name }}
						</option>
					</select>
				</div>

				<div class="input-container">
					<label for="meat">Meat type:</label>
					<select name="meat" id="meat" required v-model="meat">
						<option value="" selected disabled>Choose your meat type:</option>
						<option v-for="meat in meats" :key="meat.id" :value="meat.name">{{ meat.name }}</option>
					</select>
				</div>

				<div id="opcionals-container" class="input-container">
					<label for="opcionals"> Choose your opcionals:</label>
					<div class="checkbox-container" v-for="opcional in opcionalsData" :key="opcional.id">
						<input type="checkbox" name="opcionals" v-model="opcionals" :value="opcional.name">
						<span>{{ opcional.name }}</span>
					</div>
				</div>

				<div class="input-container">
					<input class="submit-btn" type="submit" value="Create my burger!">
				</div>
			</form>
		</div>
	</div>
</template>

<script>
import Message from './Message.vue';

export default {
	name: 'BurgerForm',
	components: {
		Message,
	},

	data() {
		return {
			// used variables initialization
			breads: null,
			meats: null,
			opcionalsData: null,
			clientName: null,
			bread: null,
			meat: null,
			opcionals: [],
			msg: null,
		};
	},
	methods: {
		/**
		 * Function that brings the ingredients from json database and associates
		 * it to variables used
		 */
		async getIngredients() {
			const req = await fetch('http://localhost:3000/ingredients');
			const data = await req.json();

			this.breads = data.breads;
			this.meats = data.meats;
			this.opcionalsData = data.opcionals;
		},

		/**
		 * Function that handle the creation of a new order based on form data
		 */
		async createOrder(e) {
			e.preventDefault();

			// prepares the data for upload
			const orderData = JSON.stringify({
				clientName: this.clientName,
				bread: this.bread,
				meat: this.meat,
				opcionals: Array.from(this.opcionals),
				status: 'Created',
			});

			// inserts the new order
			const req = await this.insertOrder(orderData);
			const res = await req.json();

			// show the success message
			this.handleMessage(`Order #${res.id} successfully created!`);

			// clears the form
			this.clearForm();
		},

		/**
		 * Function used to insert data of a new order by requesting on json api
		 */
		async insertOrder(orderData) {
			return await fetch('http://localhost:3000/orders', {
				method: 'POST',
				headers: { 'Content-Type': 'application/json' },
				body: orderData,
			});
		},

		/**
		 * Auxiliary function for setting a message for a given time
		 */
		handleMessage(message) {
			this.msg = message;
			setTimeout(() => (this.msg = ''), 3000);
		},

		/**
		 * Auxiliary function for clearing the order form
		 */
		clearForm() {
			this.clientName = '';
			this.meat = '';
			this.bread = '';
			this.opcionals = [];
		},
	},
	mounted() {
		this.getIngredients();
		this.clearForm();
	},
};
</script>

<style scoped>
#burger-form {
	max-width: 400px;
	margin: 0 auto;
}

.input-container {
	display: flex;
	flex-direction: column;
	margin-bottom: 20px;
}

.input-container label {
	font-weight: bold;
	margin-bottom: 15px;
	color: #222;
	padding: 5px 10px;
	border-left: 4px solid #fcba03;
}

.input-container input,
.input-container select {
	padding: 5px 10px;
	width: 300px;
}

#opcionals-container {
	flex-direction: row;
	flex-wrap: wrap;
}

#opcionals-container label {
	width: 100%;
}

.checkbox-container {
	display: flex;
	align-items: flex-start;
	width: 50%;
	margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
	width: auto;
}

.checkbox-container span {
	margin-left: 6px;
	font-weight: bold;
}

.submit-btn {
	background-color: #222;
	color: #fcba03;
	font-weight: bold;
	border: 2px solid #222;
	padding: 10px;
	font-size: 16px;
	margin: 0 auto;
	cursor: pointer;
	transition: 0.25s;
}

.submit-btn:hover {
	background-color: transparent;
	color: #222;
}
</style>
