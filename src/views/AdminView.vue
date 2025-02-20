<script setup>
import { Trash2, CircleCheckBig } from "lucide-vue-next";
import { ref, onMounted } from "vue";
const orders = ref([]);

const fetchOrders = async () => {
  try {
    const response = await fetch("http://127.0.0.1:3001/pedidos");
    const data = await response.json();
    console.log("AAAA");
    orders.value = data;
  } catch (error) {
    console.error("Failed to fetch orders:", error);
  }
};

const deleteOrder = async (id) => {
  try {
    await fetch(`http://127.0.0.1:3001/pedidos/${id}`, {
      method: 'DELETE'
    });
    orders.value = orders.value.filter(order => order._id !== id);
  } catch (error) {
    console.error("Failed to delete order:", error);
  }
};

const markAsDelivered = async (id) => {
  try {
    await fetch(`http://127.0.0.1:3001/pedidos/${id}`, {
      method: 'PUT',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ status: 'entregue' })
    });
    const order = orders.value.find(order => order._id === id);
    if (order) {
      order.status = 'entregue';
    }
  } catch (error) {
    console.error("Failed to update order status:", error);
  }
};


onMounted(() => {
  fetchOrders();
});
</script>

<template>
  <main class="body">
    <div class="card">
      <div class="order-list">
        <div class="order-list__title">
          <h1>Pedidos Anteriores</h1>
        </div>
        <ul class="">
          <li v-for="order in orders" :key="order.id">
            <div class="content">
              <h2>Pedido ID: {{ order._id }}</h2>
              <p>Sabores: {{ order.primeiraMetade + " e " + order.segundaMetade }}</p>
              <p>Status: {{ order.status }}</p>
            </div>

            <div class="actions">
              <button :disabled="order.status == 'entregue'" class=" check" @click="markAsDelivered(order._id)">
                <CircleCheckBig />
              </button>
              <button class="delete" @click="deleteOrder(order._id)">
                <Trash2 />
              </button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </main>
</template>

<style>
.body {
  height: calc(100vh - 200px);
  display: flex;
  padding: 20px;
  background-color: #e5c099;
  flex-grow: 1;
}

.body .card {
  width: 100%;
  height: auto;
  background-color: #fff;
  border-radius: 10px;
  display: flex;
  flex-direction: row;
  align-items: start;
  gap: 20px;
  padding: 100px;
  background-color: #3e2d1e;
}

.body .card nav {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  flex: 1;
}

.body nav a {
  padding: 0 1rem;
  background: #ebd4a4;
  font-size: 24px;
  border-radius: 99px;
  text-decoration: none;
  color: #d1853a;
  display: flex;
  justify-content: center;
  width: 100%;
  max-width: 200px;
}

nav img {
  width: 150px;
  height: 150px;
}

.order-list {
  flex: 1;
  min-height: 80%;
  background-color: #e5c099;
  padding-inline: 50px;
  padding-block: 20px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  gap: 15px;
  max-height: 100%;
}

.order-list__title {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  width: 100%;
  border-radius: 17px;
  background: #3e2d1e;
}

.order-list__title h1 {
  color: #e5c099;
  text-align: center;
  margin-block: 0px;
  padding-block: 5px;
  font-size: 21px;
}

.order-list ul {
  list-style-type: none;
  padding-inline: 0;
  background: #3e2d1e;
  border-radius: 10px;
  padding-inline: 15px;
  padding-block: 15px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  max-height: 100%;
  overflow-y: auto;
}

.order-list ul li {
  list-style-type: none;
  padding-inline: 0;
  background: #f5e0c3;
  border-radius: 8px;
  padding-inline: 8px;

  transition: opacity 0.3s ease;

  display: flex;
  justify-content: space-between;
  align-items: center;
}

.order-list ul li:hover {
  opacity: 0.7;
}

.order-list ul li h2,
.order-list ul li p {
  margin: 0;
}

.order-list ul li .actions {
  display: flex;
  align-items: center;
  gap: 7px;
}

.order-list ul li .actions button {
  width: 40px;
  height: 40px;
  color: white;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: background-color 0.3s ease, transform 0.2s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.order-list ul li .actions button:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.order-list ul li .actions button:hover:not(:disabled) {
  transform: scale(1.05);
}

.order-list ul li .actions button:active {
  transform: scale(0.9);
}

.order-list ul li .actions button.delete {
  background-color: #d32f2f;
}

.order-list ul li .actions button.check {
  background-color: #4caf50;
}

.order-list ul li .actions button:disabled {
  opacity: 0.2;
}
</style>
