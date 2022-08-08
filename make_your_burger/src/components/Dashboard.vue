<template>
	<div id ="dashboard-table">
		<Message :msg="msg" v-if="msg" />

		<div id="dashboard-table-head">
			<div class="order-id">#: </div>
			<div>Cliente</div>
			<div>Pão</div>
			<div>Carne</div>
			<div>Opcionais</div>
			<div>Ações</div>
		</div>

		<div id="dashboard-table-rows">
			<div class="dashboard-table-row" v-for="burger in burgers" :key="burger.id">
				<div class="order-number">{{ burger.id }}</div>
				<div>{{ burger.nomeCliente }}</div>
				<div>{{ burger.pao }}</div>
				<div>{{ burger.carne }}</div>
				<div>
					<ul>
						<li v-for="(opcional, index) in burger.opcionais" :key="index">
							{{ opcional }}
						</li>
					</ul>
				</div>
				<div>
					<select name="status" class="dashboard-select-status"
									@change="updateOrder($event, burger.id)"
									:disabled="burger.status == 'Finalizado'"
					>
						<option value="" disabled selected>Selecione:</option>

						<option v-for="s in status" :key="s.id" :value="s.tipo"
									 	:selected="burger.status == s.tipo"
						>
							{{ s.tipo }}
						</option>
					</select>

					<button class="cancel-btn" @click="cancelOrder(burger.id)">Cancelar</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import Message from './Message.vue';

	export default {
		name: 'Dashboard',
		components: {
			Message,
		},
		data() {
			return {
				burgers: null,
				burger_id: null,
				status: [],
				msg: null
			}
		},
		methods: {
			async getOrders() {
				const req = await fetch('http://localhost:3000/burgers');
				this.burgers = await req.json();

				this.getStatus();
			},

			async getStatus() {
				const req = await fetch('http://localhost:3000/status');
				this.status = await req.json();
			},

			async cancelOrder(orderId) {
				await fetch(`http://localhost:3000/burgers/${orderId}`,{
					method: 'DELETE'
				});

				this.handleMessage(`O pedido de nº ${orderId} foi cancelado!`);
				this.getOrders();
			},

			async updateOrder(event, orderId) {
				await fetch(`http://localhost:3000/burgers/${orderId}`, {
					method: 'PATCH',
					headers: { 'Content-Type': 'application/json' },
					body: JSON.stringify({ status: event.target.value })
				});

				this.handleMessage(`O pedido de nº ${orderId} foi atualizado!`);
			},

			handleMessage(message) {
				this.msg = message;
				setTimeout(() => (this.msg = ''), 3000);
			},
		},
		mounted() {
			this.getOrders();
		},
	};
</script>

<style scoped>
	#dashboard-table {
		max-width: 1200px;
		margin: 0 auto;
	}

	#dashboard-table-head,
	#dashboard-table-rows,
	.dashboard-table-row {
		display: flex;
		flex-wrap: wrap;
	}

	#dashboard-table-head {
		font-weight: bold;
		padding: 12px;
		border-bottom: 3px solid #333;
	}

	#dashboard-table-head div,
	.dashboard-table-row div {
		width: 19%;
	}

	#dashboard-table-head .order-id,
	.dashboard-table-row .order-number {
		width: 5%;
	}

	.dashboard-table-row {
		width: 100%;
		padding: 12px;
		border-bottom: 1px solid #ccc;
	}

	.dashboard-select-status{
		padding: 12px 6px;
		margin-right: 12px;
		background-color: transparent;
		max-width: 110px;
	}

	.dashboard-select-status,
	.cancel-btn {
		font-weight: bold;
		border: 2px solid #222;
	}

	.cancel-btn {
		background-color: #222;
		color: #fcba03;
		padding: 10px;
		font-size: 16px;
		margin: 0 auto;
		cursor: pointer;
		transition: .5s;
	}

	.cancel-btn:hover {
		background-color: transparent;
		color: #222;
	}
</style>
