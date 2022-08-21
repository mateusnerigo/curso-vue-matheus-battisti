<template>
	<div id ="dashboard-table">
		<Message :msg="msg" v-if="msg" />

		<div id="dashboard-table-head">
			<div class="order-id">#: </div>
			<div>Client</div>
			<div>Bread</div>
			<div>Meat</div>
			<div>Opcionals</div>
			<div>Actions</div>
		</div>

		<div id="dashboard-table-rows">
			<div class="dashboard-table-row" v-for="order in orders" :key="order.id">
				<div class="order-number">{{ order.id }}</div>
				<div>{{ order.clientName }}</div>
				<div>{{ order.bread }}</div>
				<div>{{ order.meat }}</div>
				<div>
					<ul>
						<li v-for="(opcional, index) in order.opcionals" :key="index">
							{{ opcional }}
						</li>
					</ul>
				</div>
				<div>
					<select name="status" class="dashboard-select-status"
									@change="updateOrder($event, order.id)"
									:disabled="order.status == 'Finished'"
					>
						<option value="" disabled selected>Choose:</option>

						<option v-for="s in status" :key="s.id" :value="s.status"
									 	:selected="order.status == s.status"
						>
							{{ s.status }}
						</option>
					</select>

					<button class="cancel-btn" @click="cancelOrder(order.id)">Cancel</button>
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
				// used variables initialization
				orders: null,
				order_id: null,
				status: [],
				msg: null
			}
		},
		methods: {
			/**
			 * Function that brings the orders made by users on BurgerForm component
			 */
			async getOrders() {
				const req = await fetch('http://localhost:3000/orders');
				this.orders = await req.json();

				// returns possible status
				this.getStatus();
			},

			/**
			 * Function that brings possible status used for display
			 */
			async getStatus() {
				const req = await fetch('http://localhost:3000/status');
				this.status = await req.json();
			},

			/**
			 * Function that handles the removing of an order by its ID
			 */
			async cancelOrder(orderId) {
				await fetch(`http://localhost:3000/orders/${orderId}`,{
					method: 'DELETE'
				});

				// show the success message
				this.handleMessage(`Order #${orderId} canceled!`);

				// calls the function that brings the orders, updating orders table
				this.getOrders();
			},

			/**
			 * Function that handles the updating of an order by its ID
			 */
			async updateOrder(event, orderId) {
				await fetch(`http://localhost:3000/orders/${orderId}`, {
					method: 'PATCH',
					headers: { 'Content-Type': 'application/json' },
					body: JSON.stringify({ status: event.target.value })
				});

				// show the success message
				this.handleMessage(`Order #${orderId} updated!`);
			},

			/**
			 * Auxiliary function for setting a message for a given time
			 */
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
