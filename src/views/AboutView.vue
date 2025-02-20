<template>
  <main class="body">
    <div class="left">
      <img src="/public/about_pic.jpeg" alt="About" id="about-pic" />
    </div>
    <div class="right">
      <h2>Nossa Historia</h2>
      <p>
        Sd Gastronomia nasceu da inquietude de um coração ansioso por praticar
        uma cozinha autêntica, honesta, reveladora e com um Q de segredos.
        Nasceu de uma mãe empreendedora e muito apegada a família. Nossa visão é
        de um modelo que trás comodidade, conveniência e segurança em
        condomínios fechados. Nosso missão é trazer um produto de extrema
        qualidade e sabor, com isso garantir a satisfação e a fidelidade de
        nossos amigos clientes.
      </p>
    </div>
  </main>
</template>

<style>
.right {
  color: #d1853a;
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: flex-end;
  gap: 20px;
  height: 550px;
}

.right h2 {
  margin: 0;
  font-size: 60px;
  text-align: right;
}

.right p {
  margin: 0;
  font-size: 20px;
  text-align: right;
  line-height: 2;
}

.left {
  width: 100%;
  display: flex;
  justify-content: center;
  height: fit-content;
  align-items: center;
}

#about-pic {
  width: 850px;
  height: 550px;
  object-fit: cover;
  object-position: 50% 10%;
}

.body {
  min-height: calc(100vh - 200px);
  display: grid;
  justify-content: center;
  align-items: center;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  padding: 20px;
  background-color: #e5c099;
  flex-grow: 1;
}

@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
