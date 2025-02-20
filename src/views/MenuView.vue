<template>
    <div class="menu">
        <div class="menu-container">
            <h1>Escolha os sabores das duas metades</h1>

            <div class="half-pizza">
                <h2>Primeira Metade</h2>
                <ul class="pizza-list">
                    <li v-for="(sabor, index) in sabores" :key="'first-' + index">
                        <label>
                            <input type="radio" name="first-half" :value="sabor" v-model="primeiraMetade" />
                            {{ sabor }}
                        </label>
                    </li>
                </ul>
            </div>

            <div class="half-pizza">
                <h2>Segunda Metade</h2>
                <ul class="pizza-list">
                    <li v-for="(sabor, index) in sabores" :key="'second-' + index">
                        <label>
                            <input type="radio" name="second-half" :value="sabor" v-model="segundaMetade" />
                            {{ sabor }}
                        </label>
                    </li>
                </ul>
            </div>

            <div class="input-group">
                <label for="nome">Nome:</label>
                <input type="text" id="nome" v-model="nome" />
            </div>

            <div class="input-group">
                <label for="endereco">Endereço:</label>
                <input type="text" id="endereco" v-model="endereco" />
            </div>

            <button @click="enviarSabores" :disabled="!primeiraMetade || !segundaMetade">
                Enviar Pedido
            </button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            sabores: [
                "Calabresa",
                "Mussarela",
                "Frango com Catupiry",
                "Portuguesa",
                "Quatro Queijos",
                "Pepperoni",
                "Margherita",
                "Chocolate",
                "Romeu e Julieta"
            ],
            selecionados: [], // Lista de sabores marcados
            primeiraMetade: "",
            segundaMetade: "",
            nome: "",
            endereco: ""
        };
    },
    methods: {
        async enviarSabores() {
            try {
                const pedido = {
                    primeiraMetade: this.primeiraMetade,
                    segundaMetade: this.segundaMetade,
                    nome: this.nome,
                    endereco: this.endereco
                };

                const response = await fetch("http://127.0.0.1:3001/pedidos", {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json"
                    },
                    body: JSON.stringify(pedido)
                });

                if (response.ok) {
                    alert("Pedido enviado com sucesso!");
                    this.primeiraMetade = "";
                    this.segundaMetade = "";
                    this.nome = "";
                    this.endereco = "";
                } else {
                    alert("Erro ao enviar pedido.");
                }
            } catch (error) {
                console.error("Erro na requisição:", error);
                alert("Erro ao conectar com o servidor.");
            }
        }
    }
};
</script>

<style scoped>
.menu {
    display: flex;
    justify-content: center;
    /* align-items: center; */
    padding: 20px;
    height: 100vh;
    background-color: #e5c099;
}

.pizza-list {
    list-style: none;
    padding: 0;
}

.pizza-list li {
    margin: 5px 0;
}

label {
    display: flex;
    align-items: center;
    cursor: pointer;
    font-size: 18px;
}

input[type="checkbox"] {
    margin-right: 10px;
    transform: scale(1.2);
    cursor: pointer;
}

button {
    margin-top: 15px;
    padding: 10px 20px;
    border: none;
    background: #264653;
    color: white;
    cursor: pointer;
    border-radius: 5px;
    transition: 0.3s;
}

button:disabled {
    background: gray;
    cursor: not-allowed;
}

button:hover:not(:disabled) {
    background: #1d3557;
}
</style>