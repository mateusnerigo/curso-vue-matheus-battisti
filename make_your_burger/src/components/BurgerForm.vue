<template>
	<div>
		<Message :msg="msg" v-if="msg" />
		<div>
			<form id="burger-form" @submit="createBurger">
				<div class="input-container">
					<label for="nomeCliente">Name:</label>
					<input type="text" name="nomeCliente" id="nomeCliente" v-model="nomeCliente" placeholder="Digite seu nome">
				</div>

				<div class="input-container">
					<label for="pao">Tipo de pão:</label>
					<select name="pao" id="pao" v-model="pao">
						<option value="" selected disabled>Escolha o tipo de pão</option>

						<option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
							{{ pao.tipo }}
						</option>
					</select>
				</div>

				<div class="input-container">
					<label for="carne">Tipo de carne:</label>
					<select name="carne" id="carne" v-model="carne">
						<option value="" selected disabled>Escolha o tipo da carne</option>
						<option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
					</select>
				</div>

				<div id="opcionais-container" class="input-container">
					<label for="opcionais"> Selecione os opcionais:</label>
					<div class="checkbox-container" v-for="opcional in opcionaisData" :key="opcional.id">
						<input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
						<span>{{ opcional.tipo }}</span>
					</div>
				</div>

				<div class="input-container">
					<input class="submit-btn" type="submit" value="Criar meu burger!">
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
				paes: null,
				carnes: null,
				opcionaisData: null,
				nomeCliente: null,
				pao: null,
				carne: null,
				opcionais: [],
				msg: null,
			};
		},
		methods: {
			async getIngredientes() {
				const req = await fetch('http://localhost:3000/ingredientes');
				const data = await req.json();

				this.paes = data.paes;
				this.carnes = data.carnes;
				this.opcionaisData = data.opcionais;
			},

			async createBurger(e) {
				e.preventDefault();

				const data = JSON.stringify({
					nomeCliente: this.nomeCliente,
					pao: this.pao,
					carne: this.carne,
					opcionais: Array.from(this.opcionais),
					status: 'Solicitado',
				});

				const req = await this.insertBurger(data);
				const res = await req.json();

				this.handleMessage(`Pedido nº ${res.id} realizado com sucesso!`);
				this.clearForm();
			},

			async insertBurger(dataInsert) {
				return await fetch('http://localhost:3000/burgers', {
					method: 'POST',
					headers: { 'Content-Type': 'application/json' },
					body: dataInsert,
				});
			},

			handleMessage(message) {
				this.msg = message;
				setTimeout(() => (this.msg = ''), 3000);
			},

			clearForm() {
				this.nomeCliente = '';
				this.carne = '';
				this.pao = '';
				this.opcionais = [];
			},
		},
		mounted() {
			this.getIngredientes();
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

	#opcionais-container {
		flex-direction: row;
		flex-wrap: wrap;
	}

	#opcionais-container label {
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
