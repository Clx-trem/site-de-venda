<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Loja CLX</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #ffffff;
      color: #000;
    }

    header {
      background: #f1f1f1;
      padding: 15px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #ccc;
    }

    .container {
      max-width: 1100px;
      margin: auto;
      padding: 20px;
    }

    #loginBox, #addProductBox {
      border: 1px solid #ccc;
      padding: 15px;
      border-radius: 10px;
      margin-bottom: 25px;
      background: #fff;
    }

    input, button {
      padding: 10px;
      margin: 5px 0;
      width: 100%;
      border-radius: 8px;
      border: 1px solid #999;
    }

    button {
      background:#000;
      color:#fff;
      cursor:pointer;
      font-weight:bold;
    }

    .product {
      border: 1px solid #ccc;
      padding: 15px;
      border-radius: 10px;
      margin-bottom: 20px;
      display:flex;
      gap:15px;
      background:#fff;
    }

    .product img {
      width:120px;
      height:120px;
      object-fit:cover;
      border-radius:8px;
      border:1px solid #aaa;
    }

    #cartBox {
      position: fixed;
      right: 10px;
      top: 10px;
      background:#fff;
      padding: 15px;
      border-radius: 10px;
      border:1px solid #ccc;
      width: 260px;
      z-index:999;
    }

    #cartItems div {
      border-bottom: 1px solid #ddd;
      padding: 5px 0;
    }
  </style>
</head>
<body>

<header>
  <h2>Loja CLX</h2>
  <button onclick="toggleLogin()">Login</button>
</header>

<div id="cartBox">
  <h3>Carrinho</h3>
  <div id="cartItems"></div>
  <strong>Total: R$ <span id="cartTotal">0.00</span></strong><br><br>
  <button onclick="finalizarCompra()">Finalizar Compra</button>
</div>

<div class="container">

  <!-- LOGIN -->
  <div id="loginBox" style="display:none;">
    <h3>Login / Cadastro</h3>
    <input id="nome" placeholder="Seu nome" />
    <input id="email" placeholder="E-mail" />
    <input id="cep" placeholder="CEP" />
    <input id="cidade" placeholder="Cidade" />
    <input id="endereco" placeholder="Endereço" />
    <button onclick="salvarLogin()">Salvar</button>
  </div>

  <!-- ADD PRODUTO -->
  <div id="addProductBox">
    <h3>Adicionar Produto</h3>
    <input id="pNome" placeholder="Nome do produto" />
    <input id="pPreco" type="number" placeholder="Preço" />
    <input id="pDescricao" placeholder="Descrição" />
    <input id="pImg" type="file" accept="image/*" />
    <button onclick="addProduto()">Adicionar</button>
  </div>

  <h2>Produtos</h2>
  <div id="produtos"></div>

</div>

<script>
let user = JSON.parse(localStorage.getItem("userCLX") || "null");
let produtos = JSON.parse(localStorage.getItem("produtosCLX") || "[]");
let carrinho = [];

function toggleLogin(){
  document.getElementById("loginBox").style.display =
    document.getElementById("loginBox").style.display === "none" ? "block" : "none";
}

function salvarLogin(){
  user = {
    nome: nome.value,
    email: email.value,
    cep: cep.value,
    cidade: cidade.value,
    endereco: endereco.value
  };
  localStorage.setItem("userCLX", JSON.stringify(user));
  alert("Login salvo!");
}

function addProduto(){
  const file = pImg.files[0];
  if(!file) return alert("Selecione uma imagem!");

  const reader = new FileReader();
  reader.onload = () => {
    const novo = {
      nome: pNome.value,
      preco: parseFloat(pPreco.value),
      descricao: pDescricao.value,
      img: reader.result
    };
    produtos.push(novo);
    localStorage.setItem("produtosCLX", JSON.stringify(produtos));
    renderProdutos();
  };
  reader.readAsDataURL(file);
}

function renderProdutos(){
  produtosDiv.innerHTML = "";
  produtos.forEach((p,i)=>{
    produtosDiv.innerHTML += `
      <div class='product'>
        <img src="${p.img}" />
        <div>
          <h3>${p.nome}</h3>
          <p>${p.descricao}</p>
          <strong>R$ ${p.preco.toFixed(2)}</strong><br><br>
          <button onclick="addCarrinho(${i})">Adicionar ao carrinho</button>
        </div>
      </div>
    `;
  });
}

function addCarrinho(i){
  carrinho.push(produtos[i]);
  renderCarrinho();
}

function renderCarrinho(){
  cartItems.innerHTML = "";
  let total = 0;

  carrinho.forEach((p, i)=>{
    total += p.preco;
    cartItems.innerHTML += `<div>${p.nome} - R$ ${p.preco.toFixed(2)}</div>`;
  });

  cartTotal.innerText = total.toFixed(2);
}

function finalizarCompra(){
  if(!user){
    alert("Você precisa fazer login para finalizar a compra!");
    return;
  }

  if(carrinho.length === 0){
    alert("Seu carrinho está vazio!");
    return;
  }

  let msg = `Olá! Quero finalizar minha compra:%0A%0A`;

  let total = 0;
  carrinho.forEach(p=>{
    msg += `• ${p.nome} - R$ ${p.preco.toFixed(2)}%0A`;
    total += p.preco;
  });

  msg += `%0ATotal: R$ ${total.toFixed(2)} (sem frete)%0A%0A`;
  msg += `Dados do cliente:%0A`;
  msg += `Nome: ${user.nome}%0AEmail: ${user.email}%0ACEP: ${user.cep}%0ACidade: ${user.cidade}%0AEndereço: ${user.endereco}`;

  window.open(`https://wa.me/5521990819172?text=${msg}`, "_blank");
}

renderProdutos();
</script>

</body>
</html>
