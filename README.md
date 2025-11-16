<!doctype html>
<html lang="pt-BR">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Loja CLX - Vendas</title>
<style>
  :root{--bg:#0f1724;--card:#0b1220;--accent:#06b6d4;--muted:#94a3b8;--text:#e6eef6}
  body{margin:0;font-family:Inter,Arial,Helvetica,sans-serif;background:linear-gradient(180deg,#071127 0%,#071225 100%);color:var(--text);min-height:100vh}
  header{display:flex;align-items:center;justify-content:space-between;padding:18px 24px;background:rgba(255,255,255,0.02);backdrop-filter:blur(6px)}
  h1{margin:0;font-size:18px}
  .container{max-width:1100px;margin:22px auto;padding:18px}
  .grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(230px,1fr));gap:14px}
  .card{background:var(--card);padding:12px;border-radius:10px;box-shadow:0 6px 18px rgba(2,6,23,0.6)}
  .product img{width:100%;height:150px;object-fit:cover;border-radius:6px}
  label{display:block;margin-top:8px;font-size:13px;color:var(--muted)}
  input[type="text"],input[type="email"],input[type="number"],textarea,select{width:100%;padding:8px;border-radius:6px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:var(--text)}
  button{background:var(--accent);color:#021028;border:0;padding:8px 12px;border-radius:8px;cursor:pointer;font-weight:600}
  .muted{color:var(--muted);font-size:13px}
  .top-actions{display:flex;gap:8px;align-items:center}
  .small{font-size:13px;padding:6px 8px;border-radius:8px}
  .cart-btn{position:relative}
  .badge{position:absolute;top:-6px;right:-6px;background:#ef4444;color:white;padding:4px 6px;border-radius:999px;font-size:12px}
  .row{display:flex;gap:12px}
  .col{flex:1}
  .products-list{margin-top:18px}
  .cart-list{max-width:480px}
  .center{text-align:center}
  .footer{margin-top:18px;color:var(--muted);font-size:13px;text-align:center}
  .product-title{font-weight:700;margin:6px 0}
  .product-price{font-weight:800}
  .actions{display:flex;gap:8px;align-items:center;margin-top:8px}
  .danger{background:#ef4444;color:white;border-radius:8px;padding:6px 8px;font-weight:700;border:0}
  .modal{position:fixed;inset:0;background:rgba(2,6,23,0.6);display:flex;align-items:center;justify-content:center;padding:18px}
  .modal .card{max-width:520px;width:100%}
  .small-muted{font-size:12px;color:var(--muted)}
  footer{margin-top:20px}
  @media(max-width:720px){.row{flex-direction:column}}
</style>
</head>
<body>

<header>
  <h1>Loja CLX</h1>
  <div class="top-actions">
    <div id="userArea" class="muted small">Não logado</div>
    <button id="toggleAddProduct" class="small">Adicionar Produto</button>
    <button id="viewCartBtn" class="small cart-btn">Carrinho <span id="cartCount" class="badge" style="display:none">0</span></button>
    <button id="logoutBtn" class="small" style="display:none">Sair</button>
  </div>
</header>

<div class="container">
  <div class="card">
    <div style="display:flex;gap:12px;align-items:center;flex-wrap:wrap">
      <div>
        <strong>Procure produtos</strong>
        <div class="small-muted">Adicione produtos abaixo ou cadastre-se para terminar a compra</div>
      </div>
      <div style="margin-left:auto">
        <input id="searchInput" placeholder="Buscar..." style="padding:8px;border-radius:8px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:var(--text)">
      </div>
    </div>
  </div>

  <!-- Add Product (visível por padrão ao clicar em 'Adicionar Produto') -->
  <div id="addProductCard" class="card" style="margin-top:12px;display:none">
    <h3>Adicionar Produto (salvo no navegador)</h3>
    <div style="display:grid;grid-template-columns:1fr 140px;gap:12px;align-items:start">
      <div>
        <label>Nome</label>
        <input id="prodName" type="text" />
        <label>Preço (R$)</label>
        <input id="prodPrice" type="number" min="0" step="0.01" />
        <label>Descrição</label>
        <textarea id="prodDesc" rows="3"></textarea>
        <label>Imagem</label>
        <input id="prodImage" type="file" accept="image/*" />
        <div style="display:flex;gap:8px;margin-top:10px">
          <button id="saveProdBtn">Salvar Produto</button>
          <button id="clearProdsBtn" class="danger">Limpar todos produtos</button>
        </div>
        <div class="small-muted" style="margin-top:8px">As imagens são salvas localmente (no seu navegador). Se carregar o site em outro dispositivo as imagens não estarão lá.</div>
      </div>
      <div id="previewWrap" class="center">
        <div style="width:120px;height:120px;border-radius:8px;background:rgba(255,255,255,0.02);display:flex;align-items:center;justify-content:center;overflow:hidden" id="imgPreview">
          <span class="small-muted">Preview</span>
        </div>
      </div>
    </div>
  </div>

  <!-- Produtos -->
  <div class="products-list">
    <h2 style="margin-bottom:8px">Produtos</h2>
    <div id="productsGrid" class="grid"></div>
  </div>

  <div class="row" style="margin-top:18px">
    <div class="col card">
      <h3>Entrar / Registrar</h3>
      <div style="display:grid;gap:8px">
        <label>Nome</label>
        <input id="userName" type="text" placeholder="Seu nome completo" />
        <label>Email</label>
        <input id="userEmail" type="email" placeholder="email@exemplo.com" />
        <label>CEP</label>
        <input id="userCEP" type="text" placeholder="00000-000" />
        <label>Cidade</label>
        <input id="userCity" type="text" placeholder="Cidade" />
        <label>Endereço</label>
        <input id="userAddress" type="text" placeholder="Rua, número, complemento..." />
        <div style="display:flex;gap:8px;margin-top:8px">
          <button id="loginBtn">Salvar / Entrar</button>
          <button id="clearAccount" class="danger">Limpar conta local</button>
        </div>
        <div class="small-muted">Os dados são armazenados localmente no navegador — ideal para um site simples sem backend.</div>
      </div>
    </div>

    <div class="col card cart-list">
      <h3>Carrinho</h3>
      <div id="cartItems"></div>
      <div id="cartSummary" style="margin-top:10px;display:none">
        <div style="display:flex;justify-content:space-between"><div>Subtotal</div><div id="subtotalVal">R$ 0,00</div></div>
        <div class="small-muted" style="margin-top:6px">Frete não incluso. Ao finalizar, o valor enviado será o total dos produtos (sem frete).</div>
        <div style="display:flex;gap:8px;margin-top:10px">
          <button id="checkoutBtn">Finalizar compra (WhatsApp)</button>
          <button id="clearCartBtn" class="danger">Limpar carrinho</button>
        </div>
      </div>
      <div id="emptyCart" class="muted" style="margin-top:6px">Carrinho vazio</div>
    </div>
  </div>

  <div class="footer">Criado por CLX — Teste localmente. Para usar em produção, hospede o arquivo e realize backups dos produtos.</div>
</div>

<!-- Modal para pedido (quando não logado ou confirmar) -->
<div id="checkoutModal" class="modal" style="display:none">
  <div class="card">
    <h3>Confirmar dados para envio</h3>
    <label>Nome</label><input id="modalName" type="text" />
    <label>Email</label><input id="modalEmail" type="email" />
    <label>CEP</label><input id="modalCEP" type="text" />
    <label>Cidade</label><input id="modalCity" type="text" />
    <label>Endereço</label><input id="modalAddress" type="text" />
    <div style="display:flex;gap:8px;margin-top:10px">
      <button id="confirmCheckoutBtn">Confirmar e enviar para WhatsApp</button>
      <button id="cancelCheckoutBtn" class="danger">Cancelar</button>
    </div>
  </div>
</div>

<script>
/* ======= UTILIDADES ======= */
const WA_NUMBER = '5521990819172'; // número em formato internacional (55 + DDD + telefone)
const STORAGE_KEYS = {PRODUCTS:'clx_products_v1', USERS:'clx_users_v1', CURRENT:'clx_current_user_v1', CART:'clx_cart_v1'};

function qs(id){return document.getElementById(id)}
function moneyBR(x){ return 'R$ ' + Number(x).toLocaleString('pt-BR',{minimumFractionDigits:2,maximumFractionDigits:2}) }

/* ======= ESTADO E ARMAZENAMENTO ======= */
let products = JSON.parse(localStorage.getItem(STORAGE_KEYS.PRODUCTS) || '[]');
let users = JSON.parse(localStorage.getItem(STORAGE_KEYS.USERS) || '{}'); // objeto por email
let currentUser = JSON.parse(localStorage.getItem(STORAGE_KEYS.CURRENT) || 'null');
let carts = JSON.parse(localStorage.getItem(STORAGE_KEYS.CART) || '{}'); // {email: {productId: qty, ...}, guest: {...}}

function persistAll(){ localStorage.setItem(STORAGE_KEYS.PRODUCTS, JSON.stringify(products)); localStorage.setItem(STORAGE_KEYS.USERS, JSON.stringify(users)); localStorage.setItem(STORAGE_KEYS.CART, JSON.stringify(carts)); localStorage.setItem(STORAGE_KEYS.CURRENT, JSON.stringify(currentUser)); }

/* ======= RENDER ======= */
function renderProducts(filter=''){
  const grid = qs('productsGrid'); grid.innerHTML='';
  const list = products.filter(p=> (p.name + ' ' + (p.desc||'')).toLowerCase().includes(filter.toLowerCase()));
  if(list.length===0){ grid.innerHTML = '<div class="muted">Nenhum produto encontrado</div>'; return; }
  list.forEach(p=>{
    const div = document.createElement('div'); div.className='card product';
    div.innerHTML = `
      <img src="${p.image || ''}" alt="${escapeHtml(p.name)}" />
      <div class="product-title">${escapeHtml(p.name)}</div>
      <div class="muted" style="min-height:36px">${escapeHtml(p.desc||'')}</div>
      <div style="display:flex;justify-content:space-between;align-items:center;margin-top:8px">
        <div class="product-price">${moneyBR(p.price)}</div>
        <div>
          <button class="small addCartBtn" data-id="${p.id}">Adicionar</button>
        </div>
      </div>
    `;
    grid.appendChild(div);
  });
  document.querySelectorAll('.addCartBtn').forEach(b=> b.addEventListener('click',()=>{
    addToCart(b.dataset.id,1);
  }));
}

function renderCart(){
  const email = currentUser?.email || 'guest';
  const cart = carts[email] || {};
  const items = Object.entries(cart);
  const wrap = qs('cartItems'); wrap.innerHTML='';
  if(items.length===0){ qs('emptyCart').style.display='block'; qs('cartSummary').style.display='none'; qs('cartCount').style.display='none'; return; }
  qs('emptyCart').style.display='none'; qs('cartSummary').style.display='block';
  let subtotal = 0;
  items.forEach(([pid,qty])=>{
    const p = products.find(x=>x.id===pid);
    if(!p) return;
    const row = document.createElement('div');
    row.style.display='flex'; row.style.gap='8px'; row.style.alignItems='center'; row.style.marginBottom='10px';
    row.innerHTML=`
      <div style="width:64px;height:64px;border-radius:6px;overflow:hidden"><img src="${p.image||''}" style="width:100%;height:100%;object-fit:cover"></div>
      <div style="flex:1">
        <div style="font-weight:700">${escapeHtml(p.name)}</div>
        <div class="small-muted">${moneyBR(p.price)} x ${qty} = <strong>${moneyBR(p.price * qty)}</strong></div>
      </div>
      <div style="display:flex;flex-direction:column;gap:6px;align-items:flex-end">
        <div style="display:flex;gap:6px">
          <button class="small decBtn" data-id="${pid}">-</button>
          <div class="small">${qty}</div>
          <button class="small incBtn" data-id="${pid}">+</button>
        </div>
        <button class="small danger rmBtn" data-id="${pid}">Remover</button>
      </div>
    `;
    wrap.appendChild(row);
    subtotal += p.price * qty;
  });
  qs('subtotalVal').textContent = moneyBR(subtotal);
  qs('cartSummary').style.display = 'block';
  qs('cartCount').textContent = items.reduce((s,[,q])=>s+q,0);
  qs('cartCount').style.display = 'inline-block';

  // eventos
  wrap.querySelectorAll('.incBtn').forEach(b=> b.onclick = ()=> { changeQty(b.dataset.id, +1); });
  wrap.querySelectorAll('.decBtn').forEach(b=> b.onclick = ()=> { changeQty(b.dataset.id, -1); });
  wrap.querySelectorAll('.rmBtn').forEach(b=> b.onclick = ()=> { removeFromCart(b.dataset.id); });
}

function renderUserArea(){
  const area = qs('userArea');
  if(currentUser){
    area.textContent = `${currentUser.name} • ${currentUser.email}`;
    qs('logoutBtn').style.display='inline-block';
  } else {
    area.textContent = 'Não logado';
    qs('logoutBtn').style.display='none';
  }
}

/* ======= PRODUTOS CRUD (local) ======= */
function addProductObj(obj){
  products.unshift(obj);
  persistAll(); renderProducts(qs('searchInput').value); renderCart();
}

function generateId(){ return 'p_' + Math.random().toString(36).slice(2,9); }

qs('toggleAddProduct').addEventListener('click', ()=> {
  const el = qs('addProductCard'); el.style.display = el.style.display === 'none' ? 'block' : 'none';
});

qs('prodImage').addEventListener('change', async (ev)=>{
  const file = ev.target.files[0];
  if(!file) return;
  const data = await fileToDataURL(file);
  qs('imgPreview').innerHTML = `<img src="${data}" style="width:100%;height:100%;object-fit:cover">`;
  qs('imgPreview').dataset.img = data;
});

qs('saveProdBtn').addEventListener('click', ()=>{
  const name = qs('prodName').value.trim();
  const price = parseFloat(qs('prodPrice').value || 0);
  const desc = qs('prodDesc').value.trim();
  const img = qs('imgPreview').dataset.img || '';
  if(!name || !price){ alert('Nome e preço são obrigatórios'); return; }
  const newP = { id: generateId(), name, price, desc, image: img, createdAt: Date.now() };
  addProductObj(newP);
  qs('prodName').value=''; qs('prodPrice').value=''; qs('prodDesc').value=''; qs('prodImage').value=''; qs('imgPreview').innerHTML = '<span class="small-muted">Preview</span>'; delete qs('imgPreview').dataset.img;
  alert('Produto adicionado com sucesso!');
});

qs('clearProdsBtn').addEventListener('click', ()=>{
  if(!confirm('Limpar TODOS os produtos salvos localmente?')) return;
  products = []; persistAll(); renderProducts(); renderCart();
});

/* ======= CARRINHO ======= */
function getCartFor(email){ return carts[email] = (carts[email] || {}); }

function addToCart(pid, qty=1){
  const email = currentUser?.email || 'guest';
  const cart = getCartFor(email);
  cart[pid] = (cart[pid] || 0) + qty;
  if(cart[pid] <= 0) delete cart[pid];
  persistAll(); renderCart();
}

function changeQty(pid, delta){
  const email = currentUser?.email || 'guest';
  const cart = getCartFor(email);
  cart[pid] = (cart[pid] || 0) + delta;
  if(cart[pid] <= 0) delete cart[pid];
  persistAll(); renderCart();
}

function removeFromCart(pid){
  const email = currentUser?.email || 'guest';
  const cart = getCartFor(email);
  delete cart[pid];
  persistAll(); renderCart();
}

qs('clearCartBtn').addEventListener('click', ()=> {
  const email = currentUser?.email || 'guest';
  if(!confirm('Limpar carrinho?')) return;
  carts[email] = {}; persistAll(); renderCart();
});

/* ======= LOGIN / REGISTRO (local) ======= */
qs('loginBtn').addEventListener('click', ()=>{
  const name = qs('userName').value.trim();
  const email = qs('userEmail').value.trim().toLowerCase();
  const cep = qs('userCEP').value.trim();
  const city = qs('userCity').value.trim();
  const address = qs('userAddress').value.trim();
  if(!email || !name){ alert('Nome e Email são obrigatórios'); return; }
  users[email] = { name, email, cep, city, address };
  currentUser = { name, email, cep, city, address };
  persistAll();
  renderUserArea(); alert('Usuário salvo e logado localmente!');
});

qs('logoutBtn').addEventListener('click', ()=> {
  currentUser = null; persistAll(); renderUserArea(); renderCart();
});

qs('clearAccount').addEventListener('click', ()=> {
  if(!confirm('Remover seus dados locais?')) return;
  if(currentUser){ delete users[currentUser.email]; currentUser = null; }
  persistAll(); renderUserArea(); alert('Dados locais removidos');
});

/* ======= BUSCA ======= */
qs('searchInput').addEventListener('input', (e)=> renderProducts(e.target.value));

/* ======= CHECKOUT -> WhatsApp ======= */
qs('checkoutBtn').addEventListener('click', ()=> {
  // se não houver items, não faz nada
  const email = currentUser?.email || 'guest';
  const cart = carts[email] || {};
  if(Object.keys(cart).length === 0){ alert('Seu carrinho está vazio'); return; }
  // Se não estiver logado, pedir dados no modal
  if(!currentUser){
    // prefill modal with guest saved if any
    qs('modalName').value = '';
    qs('modalEmail').value = '';
    qs('modalCEP').value = '';
    qs('modalCity').value = '';
    qs('modalAddress').value = '';
    qs('checkoutModal').style.display = 'flex';
    return;
  }
  // se estiver logado, confirmar e enviar
  sendOrderToWhatsApp(currentUser);
});

qs('confirmCheckoutBtn').addEventListener('click', ()=> {
  const name = qs('modalName').value.trim();
  const email = qs('modalEmail').value.trim();
  const cep = qs('modalCEP').value.trim();
  const city = qs('modalCity').value.trim();
  const address = qs('modalAddress').value.trim();
  if(!name || !email){ alert('Nome e email são obrigatórios'); return; }
  // salvar como usuário temporário (não sobrescreve se já existir)
  users[email.toLowerCase()] = { name, email, cep, city, address };
  currentUser = { name, email: email.toLowerCase(), cep, city, address };
  persistAll(); qs('checkoutModal').style.display = 'none'; renderUserArea(); sendOrderToWhatsApp(currentUser);
});

qs('cancelCheckoutBtn').addEventListener('click', ()=> qs('checkoutModal').style.display = 'none');

function sendOrderToWhatsApp(user){
  const email = user.email || 'guest';
  const cart = carts[email] || {};
  if(Object.keys(cart).length===0){ alert('Carrinho vazio'); return; }
  let subtotal = 0;
  let lines = [];
  for(const [pid,qty] of Object.entries(cart)){
    const p = products.find(x=>x.id===pid);
    if(!p) continue;
    lines.push(`${p.name} x${qty} — ${moneyBR(p.price * qty)}`);
    subtotal += p.price * qty;
  }
  const msg = [
    `*Novo pedido*`,
    ``,
    `*Cliente:* ${user.name}`,
    `*Email:* ${user.email}`,
    `*Endereço:* ${user.address || '-'} / ${user.city || '-'} / CEP: ${user.cep || '-'}`,
    ``,
    `*Itens:*`,
    ...lines,
    ``,
    `*Total (produtos):* ${moneyBR(subtotal)}`,
    `*Observação:* Valor do frete NÃO incluso — combinar via WhatsApp.`,
    ``,
    `Por favor confirme disponibilidade e envio.`
  ].join('\n');
  const encoded = encodeURIComponent(msg);
  const url = `https://wa.me/${WA_NUMBER}?text=${encoded}`;
  // abrir WhatsApp
  window.open(url, '_blank');
}

/* ======= AUX ======= */
function fileToDataURL(file){
  return new Promise((res,rej)=>{
    const reader = new FileReader();
    reader.onload = ()=> res(reader.result);
    reader.onerror = rej;
    reader.readAsDataURL(file);
  });
}

function escapeHtml(s){ if(!s) return ''; return s.replace(/[&<>"']/g, c=>({ '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;' }[c])); }

/* ======= INICIALIZAÇÃO ======= */
// Se não existirem produtos, criar alguns de exemplo
if(products.length===0){
  products = [
    { id: generateId(), name:'Camiseta CLX', price:59.9, desc:'Camiseta de algodão - tamanhos P/M/G', image:'', createdAt:Date.now() },
    { id: generateId(), name:'Caneca Criativa', price:34.5, desc:'Caneca cerâmica 300ml', image:'', createdAt:Date.now() }
  ];
  persistAll();
}
renderProducts();
renderUserArea();
renderCart();

/* ======= carregar campos do login se user já salvo ======= */
if(currentUser){
  qs('userName').value = currentUser.name || '';
  qs('userEmail').value = currentUser.email || '';
  qs('userCEP').value = currentUser.cep || '';
  qs('userCity').value = currentUser.city || '';
  qs('userAddress').value = currentUser.address || '';
}

/* ======= extra: botao ver carrinho ======= */
qs('viewCartBtn').addEventListener('click', ()=> {
  window.scrollTo({top: document.body.scrollHeight, behavior:'smooth'});
});

/* ======= btn logout already exists ======= */

</script>
</body>
</html>
