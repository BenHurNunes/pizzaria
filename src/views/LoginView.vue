<template>
  <div class="login">
    <div class="container">
      <h1>Login</h1>
      <form @submit.prevent="login">
        <div class="input-group">
          <label for="username">Usuário:</label>
          <input type="text" id="username" v-model="username" required />
        </div>
        <div class="input-group">
          <label for="password">Senha:</label>
          <input type="password" id="password" v-model="password" required />
        </div>
        <button type="submit">Entrar</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      password: ""
    };
  },
  methods: {
    async login() {
      try {
        const user = {
          username: this.username,
          password: this.password,
        };

        const response = await fetch("http://127.0.0.1:3001/auth/login", {
          method: "POST",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify(user)
        });

        if (response.ok) {
          alert("Login feito!");
          window.location.href = "/admin";
        } else {
          alert("Erro ao logar.");
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
.container {
  border-radius: 20px;
  background-color: #3e2d1e;
  padding: 20px;
  width: 100%;
  max-width: 400px;
  color: #e5c099;
}

.login {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: calc(100vh - 190px);
  background-color: #e5c099;
}

.input-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input {
  padding: 10px;
  width: 100%;
  max-width: 300px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 10px 20px;
  border: none;
  background: #264653;
  color: white;
  cursor: pointer;
  border-radius: 5px;
  transition: 0.3s;
}

button:hover {
  background: #1d3557;
}
</style>
