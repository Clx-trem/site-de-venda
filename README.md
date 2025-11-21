<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Site De Vendas - Loja CLX</title>

<!-- Swiper.js -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.css"/>
<script src="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.js"></script>

<style>
:root { --accent:#ff6b6b; --accent2:#ff9a76; --card-bg:#ffffff; --dark:#0f1724; }
*{box-sizing:border-box;margin:0;padding:0;font-family:Inter,system-ui,Arial,sans-serif}
body{background:#fff;color:var(--dark);line-height:1.5;}
header{background:linear-gradient(90deg,var(--accent),var(--accent2));color:white;text-align:center;padding:18px 16px;position:fixed;top:0;left:0;right:0;z-index:1000;border-bottom:4px solid rgba(0,0,0,0.06);}
header h1{font-size:22px;margin-bottom:2px}
header p{margin:0;font-size:13px;opacity:0.95}
main{padding:120px 16px 40px;max-width:1100px;margin:0 auto}
.fundo-branco{background:#fff;display:inline-block;padding:6px 12px;border-radius:8px;margin-bottom:16px;color:#111}
.pricing{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:16px}
.pkg{background:var(--card-bg);border-radius:12px;box-shadow:0 6px 18px rgba(2,6,23,0.08);overflow:hidden;display:flex;flex-direction:column;text-align:center;transition:transform .15s}
.pkg:hover{transform:translateY(-6px)}
.pkg .swiper{width:100%;height:220px}
.pkg .swiper-slide img{width:100%;height:220px;object-fit:cover}
.pkg-content{padding:12px;flex:1;display:flex;flex-direction:column;justify-content:space-between}
.pkg-content h3{font-size:16px;margin-bottom:6px}
.pkg-content .price{color:var(--accent);font-weight:800;margin-bottom:8px}
.etiquetas{display:flex;flex-wrap:wrap;justify-content:center;gap:6px;margin-bottom:10px}
.etiqueta{background:#eef2ff;color:#111;font-size:12px;border-radius:6px;padding:4px 8px;font-weight:600}
.pkg-content ul{list-style:none;margin:0;padding:0;text-align:left}
.pkg-content ul li{font-size:13px;margin-bottom:6px}
.cta{display:inline-block;margin-top:8px;background:var(--accent);color:#fff;padding:8px 12px;border-radius:8px;text-decoration:none;font-weight:700;cursor:pointer}
.avisos{margin-top:40px;background:#fff;border-radius:12px;padding:16px;box-shadow:0 6px 18px rgba(2,6,23,0.06)}
.avisos h3{margin-bottom:8px;color:var(--accent)}
.floating-buttons{position:fixed;bottom:20px;right:20px;display:flex;gap:12px;z-index:10000}
.floating-buttons a{width:56px;height:56px;border-radius:50%;display:flex;align-items:center;justify-content:center;box-shadow:0 6px 20px rgba(2,6,23,0.2);transition:transform .15s}
.floating-buttons a img{width:28px;height:28px}
.floating-buttons a:hover{transform:scale(1.06)}
.floating-buttons a.whatsapp{background:#25D366}
#cart-icon{position:fixed;bottom:90px;right:20px;width:60px;height:60px;background:var(--accent);border-radius:50%;display:flex;align-items:center;justify-content:center;cursor:pointer;box-shadow:0 6px 20px rgba(0,0,0,0.2);z-index:10001;}
#cart-icon img{width:30px;height:30px;}
#cart-panel{position:fixed;bottom:20px;right:90px;width:320px;max-height:500px;background:#fff;border-radius:12px;box-shadow:0 8px 30px rgba(0,0,0,0.2);overflow-y:auto;padding:12px;display:none;flex-direction:column;z-index:10001;}
#cart-panel h3{margin-bottom:8px;color:var(--accent)}
.cart-item{display:flex;justify-content:space-between;margin-bottom:8px;border-bottom:1px solid #eee;padding-bottom:6px}
.cart-item span{font-size:14px}
.remove-btn{cursor:pointer;color:#ff4d4d;font-weight:700;font-size:14px}
#checkout-btn{margin-top:8px;padding:8px;background:var(--accent);color:#fff;border:none;border-radius:8px;cursor:pointer;font-weight:700}
#checkout-form{display:none;flex-direction:column;margin-top:8px}
#checkout-form input{margin-bottom:8px;padding:6px 8px;border:1px solid #ccc;border-radius:6px;font-size:14px}
#checkout-form button{padding:8px;background:var(--accent);color:#fff;border:none;border-radius:8px;cursor:pointer;font-weight:700}
</style>
</head>
<body>

<header>
  <h1>Site De Vendas</h1>
  <p>Vendas — De artesanato</p>
</header>

<main>
  <h2 class="fundo-branco">Artesanato</h2>
  <div class="pricing">
    <div class="pkg" data-name="artesanato 1" data-price="60">
      <div class="swiper pacoteSwiper">
        <div class="swiper-wrapper">
          <div class="swiper-slide"><img src="artesanato10a.jpg" alt="artesanato 1"></div>
          <div class="swiper-slide"><img src="artesanato10b.jpg" alt="artesanato 2"></div>
        </div>
        <div class="swiper-pagination"></div>
      </div>
      <div class="pkg-content">
        <h3>Artesanato</h3>
        <div class="price">R$ 60</div>
        <div class="etiquetas">
          <span class="etiqueta">Entrega Fácil</span>
          <span class="etiqueta">Frete Grátis</span>
        </div>
        <ul>
          <li>artesanato</li>
          <li>Qualidade premium</li>
          <li>Envio combinado pelo WhatsApp</li>
        </ul>
        <a class="cta add-to-cart">Adicionar ao Carrinho</a>
      </div>
    </div>
    <div class="pkg" data-name="Kit com 20 Pelúcias" data-price="280">
      <div class="swiper pacoteSwiper">
        <div class="swiper-wrapper">
          <div class="swiper-slide"><img src="pelucia20a.jpg" alt="Kit 20 pelúcias - 1"></div>
          <div class="swiper-slide"><img src="pelucia20b.jpg" alt="Kit 20 pelúcias - 2"></div>
        </div>
        <div class="swiper-pagination"></div>
      </div>
      <div class="pkg-content">
        <h3>Kit com 20 Pelúcias</h3>
        <div class="price">R$ 280</div>
        <div class="etiquetas">
          <span class="etiqueta">Entrega Fácil</span>
          <span class="etiqueta">Frete Grátis</span>
        </div>
        <ul>
          <li>20 pelúcias variadas</li>
          <li>Alta qualidade e acabamento</li>
          <li>Envio combinado pelo WhatsApp</li>
        </ul>
        <a class="cta add-to-cart">Adicionar ao Carrinho</a>
      </div>
    </div>

  </div>

  <!-- Seção de Informações Importantes -->
  <div class="avisos">
    <h3>Informações importantes</h3>
    <p>Tempo de locação: 4 horas. Caso precise de horário estendido ou transporte fora das regiões atendidas, entre em contato.</p>
    
    <h3>Como comprar</h3>
    <ol>
      <li>Entre em contato por WhatsApp: <a href="https://wa.me/5521990819172" target="_blank">(21) 99081-9172</a></li>
      <li>Combine o kit e o endereço de entrega.</li>
      <li>Pagamento: na hora da entrega.</li>
    </ol>
  </div>
</main>

<!-- Floating WhatsApp -->
<div class="floating-buttons">
  <a href="https://wa.me/5521990819172" target="_blank" class="whatsapp">
    <img src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg" alt="WhatsApp">
  </a>
</div>

<!-- Carrinho flutuante -->
<div id="cart-icon">
  <img src="https://cdn-icons-png.flaticon.com/512/263/263142.png" alt="Carrinho">
</div>
<div id="cart-panel">
  <h3>Carrinho</h3>
  <div id="cart-items"></div>
  <div><strong>Total: R$ <span id="cart-total">0</span></strong></div>
  <button id="checkout-btn">Finalizar Compra</button>

  <!-- Formulário de finalização -->
  <div id="checkout-form">
    <input type="text" id="customer-name" placeholder="Nome completo">
    <input type="text" id="customer-address" placeholder="Endereço completo">
    <input type="text" id="customer-cep" placeholder="CEP">
    <button id="submit-order">Enviar Pedido</button>
  </div>
</div>

<footer>
  © CasaRes Play — Aluguel e venda de pelúcias.<br>
  Contato: (21) 99081-9172 — casaresplayfesta@gmail.com
</footer>

<script>
document.querySelectorAll('.pacoteSwiper').forEach((swiperEl)=>{
  new Swiper(swiperEl, { loop:true, autoplay:{delay:5000,disableOnInteraction:false}, slidesPerView:1, spaceBetween:0, pagination:{el:swiperEl.querySelector('.swiper-pagination'), clickable:true}});
});

// Carrinho
let cart=[];
const cartIcon=document.getElementById('cart-icon');
const cartPanel=document.getElementById('cart-panel');
const cartItems=document.getElementById('cart-items');
const cartTotal=document.getElementById('cart-total');
const checkoutBtn=document.getElementById('checkout-btn');
const checkoutForm=document.getElementById('checkout-form');
const submitOrder=document.getElementById('submit-order');

function renderCart(){
  cartItems.innerHTML='';
  let total=0;
  cart.forEach((item,index)=>{
    total+=item.price*item.qty;
    const div=document.createElement('div');
    div.className='cart-item';
    div.innerHTML=`<span>${item.name} x${item.qty}</span> <span>R$ ${item.price*item.qty}</span> <span class="remove-btn" data-index="${index}">X</span>`;
    cartItems.appendChild(div);
  });
  cartTotal.textContent=total;
  document.querySelectorAll('.remove-btn').forEach(btn=>{
    btn.onclick=()=>{ cart.splice(btn.dataset.index,1); renderCart();}
  });
}

document.querySelectorAll('.add-to-cart').forEach(btn=>{
  btn.onclick=()=>{
    const pkg=btn.closest('.pkg');
    const name=pkg.dataset.name;
    const price=parseFloat(pkg.dataset.price);
    let existing=cart.find(i=>i.name===name);
    if(existing){ existing.qty+=1; } else { cart.push({name,price,qty:1}); }
    renderCart();
    cartPanel.style.display='flex';
  };
});

cartIcon.onclick=()=>{ cartPanel.style.display=cartPanel.style.display==='flex'?'none':'flex'; }

checkoutBtn.onclick=()=>{
  if(cart.length===0){ alert('Carrinho vazio!'); return; }
  checkoutForm.style.display='flex';
};

submitOrder.onclick=()=>{
  const name=document.getElementById('customer-name').value.trim();
  const address=document.getElementById('customer-address').value.trim();
  const cep=document.getElementById('customer-cep').value.trim();
  if(!name || !address || !cep){ alert('Preencha todos os campos!'); return; }
  let message='Olá! Quero comprar:%0A';
  cart.forEach(i=>{ message+=`${i.name} x${i.qty} = R$ ${i.price*i.qty}%0A`; });
  message+=`Total: R$ ${cart.reduce((acc,i)=>acc+i.price*i.qty,0)}%0ANome: ${name}%0AEndereço: ${address}%0ACEP: ${cep}`;
  window.open(`https://wa.me/5521990819172?text=${message}`,'_blank');
};
</script>

</body>
</html>
