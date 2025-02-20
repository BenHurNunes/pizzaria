<template>
  <main class="body">
    <div class="left">
      <div class="buttons">
        <a href="/menu" class="btn">FAÇA SEU PEDIDO</a>
        <!-- <a href="#" class="btn">PROMOÇÕES</a> -->
      </div>
    </div>
    <div class="right">
      <div class="card">
        <div class="section">
          <h3>MENU DIGITAL</h3>
          <p>Com o menu digital, você pode escolher entre as mais variadas pizzas do nosso estabelecimento assim como
            bordas e adicionais a sua vontade!</p>
        </div>
        <div class="divider"></div>
        <div class="section">
          <h3>PROMOÇÕES</h3>
          <p>Além das nossas mais variadas opções de pizza, ainda temos promoções novas a todo momento, não esqueça de
            conferi-las.</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.body {
  height: calc(100vh - 200px);
  display: grid;
  justify-content: center;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  padding: 20px;
  background-color: #e5c099;
  flex-grow: 1;
  align-items: center;
}

.left {
  width: 100%;
  display: flex;
  justify-content: center;
  height: 100%;
  align-items: center;
}

.buttons{
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center; 
  width: fit-content;
  height: 50%;
  gap: 20px;
}

.btn {
  width: 20rem;
  background-color: #3e2d1e;
  color: white;
  border: none;
  padding: 15px;
  cursor: pointer;
  border-radius: 8px;
  text-decoration: none;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 40px;
  cursor: pointer;
  font-size: 1.4rem;
}

.right {
  height: 80%;
  display: flex;
  justify-content: center;
}

.card {
  position: relative;
  right: -20px;
  background: #3e2d1e;
  padding: 20px 60px;
  border-radius: 10px 0 0 10px;
  color: white;
  display: flex;
  justify-content: space-between;
}

.section {
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 20px;
  justify-content: center;
  padding: 0 10px;
}

.section h3{
  font-size: 2rem;
  margin: 0;
}

.section p{
  font-size: 1.2rem;
  margin: 0;
}

.divider {
  width: 2px;
  background: white;
}
</style>
