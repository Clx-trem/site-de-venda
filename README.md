<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>CasaRes Play - Loja CLX (Adaptado)</title>

<!-- Swiper.js -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.css"/>
<script src="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.js"></script>

<style>
:root { --accent:#ff6b6b; --accent2:#ff9a76; --dark:#0f1724; --muted:#6b7280; --card-bg:#ffffff; }
*{box-sizing:border-box;margin:0;padding:0;font-family:Inter,system-ui,Arial,sans-serif}
html,body{height:100%}
body{
  background: url('fundo.jpg') no-repeat center center fixed;
  background-size: cover;
  color:var(--dark);
  line-height:1.5;
  -webkit-font-smoothing:antialiased;
}
header{
  background:linear-gradient(90deg,var(--accent),var(--accent2));
  color:white;text-align:center;padding:18px 16px;position:fixed;top:0;left:0;right:0;z-index:1000;border-bottom:4px solid rgba(0,0,0,0.06);
}
header .topbar{display:flex;align-items:center;gap:12px;max-width:1100px;margin:0 auto}
header h1{font-size:22px;margin-bottom:2px}
header p{margin:0;font-size:13px;opacity:0.95}
main{padding:120px 16px 40px;max-width:1100px;margin:0 auto}
.fundo-branco{background:#fff;display:inline-block;padding:6px 12px;border-radius:8px;margin-bottom:16px;color:#111}
.aviso-indisponivel{background:#fff3cd;border:1px solid #ffeeba;color:#856404;padding:16px;border-radius:12px;text-align:center;margin-bottom:30px;font-weight:600;box-shadow:0 4px 10px rgba(0,0,0,0.08)}
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
.cta.indisponivel{opacity:0.6;cursor:not-allowed}
.avisos{margin-top:40px;background:#fff;border-radius:12px;padding:16px;box-shadow:0 6px 18px rgba(2,6,23,0.06)}
.avisos h3{margin-bottom:8px;color:var(--accent)}
.floating-buttons{position:fixed;bottom:20px;right:20px;display:flex;gap:12px;z-index:10000}
.floating-buttons a{width:56px;height:56px;border-radius:50%;display:flex;align-items:center;justify-content:center;box-shadow:0 6px 20px rgba(2,6,23,0.2);transition:transform .15s}
.floating-buttons a img{width:28px;height:28px}
.floating-buttons a:hover{transform:scale(1.06)}
.floating-buttons a.whatsapp{background:#25D366}
.floating-buttons a.instagram{background: radial-gradient(circle at 30% 107%, #fdf497 0%, #fd5949 45%, #d6249f 60%, #285AEB 90%)}

/* Admin / Add product panel */
.admin-panel{position:fixed;left:20px;top:92px;background:rgba(255,255,255,0.98);padding:12px;border-radius:10px;box-shadow:0 6px 20px rgba(2,6,23,0.12);z-index:800;min-width:300px}
.admin-panel h4{margin-bottom:8px}
.admin-panel input, .admin-panel textarea, .admin-panel button{width:100%;margin-bottom:8px;padding:8px;border-radius:8px;border:1px solid #ddd}
.small-muted{font-size:12px;color:var(--muted)}

/* Cart */
.cart-fab{position:fixed;bottom:20px;left:20px;background:linear-gradient(90deg,var(--accent),var(--accent2));color:#fff;padding:12px 14px;border-radius:12px;box-shadow:0 12px 30px rgba(2,6,23,0.18);z-index:10001;cursor:pointer}
.badge{background:#111;color:#fff;padding:6px 8px;border-radius:999px;margin-left:8px;font-weight:700}

/* responsive tweaks */
@media(max-width:720px){.admin-panel{position:static;width:auto;margin-bottom:12px}}
</style>
</head>
<body>

<header>
  <div class="topbar">
    <div style="flex:1;text-align:left;padding-left:8px">
      <h1>CasaRes Play</h1>
      <p style="font-size:12px;margin-top:6px">Aluguel e venda de pelúcias — diversão garantida!</p>
    </div>
    <div style="display:flex;gap:8px;align-items:center">
      <div id="userArea" class="small-muted">Não logado</div>
      <button id="btnToggleAdmin" style="background:rgba(255,255,255,0.12);color:#fff;border:0;padding:8px 10px;border-radius:8px;cursor:pointer">Adicionar Produto</button>
    </div>
  </div>
</header>

<!-- Admin panel (adicionar produtos pelo site) -->
<div id="adminPanel" class="admin-panel" style="display:none">
  <h4>Adicionar Produto</h4>
  <input id="pName" placeholder="Nome do produto" />
  <input id="pPrice" type="number" placeholder="Preço (ex: 150.00)" />
  <input id="pTags" placeholder="Etiquetas (separadas por vírgula)" />
  <textarea id="pDesc" rows="3" placeholder="Descrição curta"></textarea>
  <label class="small-muted">Imagens (escolha várias)</label>
  <input id="pImgs" type="file" accept="image/*" multiple />
  <button id="saveProductBtn">Salvar produto</button>
  <button id="clearAllBtn" style="background:#ef4444;color:white">Limpar todos produtos</button>
  <div class="small-muted">As imagens ficam salvas localmente no seu navegador (localStorage). Para uso em produção, use um servidor/armazenamento.</div>
</div>

<main>

  <div class="aviso-indisponivel">
    🚫 <strong>AVISO:</strong> A locação de máquinas está temporariamente <strong>indisponível</strong> — pacotes com máquina estão apenas para visualização. Você pode comprar pelúcias normalmente.
  </div>

  <h2 class="fundo-branco">Pacotes com máquina (4 horas)</h2>
  <div id="pacotes" class="pricing"></div>

  <h2 class="fundo-branco" style="margin-top:40px">Venda de Pelúcias 🧸</h2>
  <div id="vendas" class="pricing"></div>

  <div class="avisos">
    <h3>Informações importantes</h3>
    <p>Tempo de locação: 4 horas. Caso precise de horário estendido ou transporte fora das regiões atendidas, entre em contato.</p>
    <h3>Onde entregamos</h3>
    <p>Paracambi, Seropédica, Japeri e Conrado — frete grátis nessas localidades (exemplo).</p>
    <h3>Como comprar</h3>
    <ol>
      <li>Adicione ao carrinho e finalize — você será levado ao WhatsApp.</li>
      <li>Combine o envio e o frete pelo WhatsApp.</li>
      <li>Pagamento: acordado pelo WhatsApp.</li>
    </ol>
  </div>

</main>

<!-- Floating buttons -->
<div class="floating-buttons">
  <a id="waBtn" class="whatsapp" target="_blank" title="WhatsApp">
    <img src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg" alt="WhatsApp">
  </a>
  <a href="https://www.instagram.com/" target="_blank" class="instagram" title="Instagram">
    <img src="https://upload.wikimedia.org/wikipedia/commons/a/a5/Instagram_icon.png" alt="Instagram">
  </a>
</div>

<!-- Cart FAB -->
<div id="cartFab" class="cart-fab">Carrinho <span id="cartBadge" class="badge" style="display:none">0</span></div>

<!-- Checkout modal (simple) -->
<div id="checkoutModal" style="display:none;position:fixed;inset:0;background:rgba(2,6,23,0.5);align-items:center;justify-content:center;z-index:20000">
  <div style="background:#fff;padding:16px;border-radius:10px;max-width:520px;width:92%;margin:auto">
    <h3>Confirmar dados</h3>
    <input id="cName" placeholder="Nome completo" />
    <input id="cEmail" placeholder="Email" />
    <input id="cCEP" placeholder="CEP" />
    <input id="cCity" placeholder="Cidade" />
    <input id="cAddress" placeholder="Endereço" />
    <div style="display:flex;gap:8px;margin-top:10px">
      <button id="confirmOrderBtn">Confirmar e abrir WhatsApp</button>
      <button id="cancelOrderBtn" style="background:#ef4444;color:#fff">Cancelar</button>
    </div>
  </div>
</div>

<script>
const WA_NUMBER = '5521990819172'; // seu número (55 + DDD + telefone)
const STORAGE_PRODUCTS = 'clx_products_v2';
const STORAGE_USERS = 'clx_users_v2';
const STORAGE_CART = 'clx_cart_v2';

// Estado
let products = JSON.parse(localStorage.getItem(STORAGE_PRODUCTS) || 'null');
if(!products){
  // produtos de exemplo inspirados no modelo
  products = [
    { id: 'pkg30', type:'pacote', title:'30 pelúcias + máquina', price:1000, tags:['Frete Grátis','4 horas'], desc:'30 pelúcias inclusas. Uso da máquina por 4 horas.', images:[] , available:false},
    { id: 'pkg50', type:'pacote', title:'50 pelúcias + máquina', price:1300, tags:['Frete Grátis','4 horas'], desc:'50 pelúcias inclusas. Uso da máquina por 4 horas.', images:[], available:false},
    { id: 'pkgMachine', type:'pacote', title:'Somente Máquina (4h)', price:550, tags:['4 horas','Montagem inclusa'], desc:'Uso da máquina por 4 horas. Sem pelúcias inclusas.', images:[], available:false},
    { id: 'pkgCustom', type:'pacote', title:'Pacote Personalizado', price:0, tags:[], desc:'Monte seu pacote conforme sua festa.', images:[], available:false},
    { id: 'kit10', type:'venda', title:'Kit com 10 Pelúcias', price:150, tags:['Entrega Fácil','Frete Grátis'], desc:'10 pelúcias sortidas - qualidade premium.', images:[], available:true},
    { id: 'kit20', type:'venda', title:'Kit com 20 Pelúcias', price:280, tags:['Entrega Fácil','Frete Grátis'], desc:'20 pelúcias variadas - acabamento premium.', images:[], available:true}
  ];
  localStorage.setItem(STORAGE_PRODUCTS, JSON.stringify(products));
}

let cart = JSON.parse(localStorage.getItem(STORAGE_CART) || '{}'); // { productId: qty }
let currentUser = JSON.parse(localStorage.getItem(STORAGE_USERS) || 'null');

// Helpers
function money(x){ return 'R$ ' + Number(x).toLocaleString('pt-BR',{minimumFractionDigits:2,maximumFractionDigits:2}); }
function qs(sel){return document.querySelector(sel)}
function qsa(sel){return Array.from(document.querySelectorAll(sel))}

// Render
function renderAll(){ renderSections(); renderCartBadge(); }

function renderSections(){
  const pacotesEl = qs('#pacotes'); pacotesEl.innerHTML = '';
  const vendasEl = qs('#vendas'); vendasEl.innerHTML = '';
  products.forEach(p=>{
    const card = document.createElement('div'); card.className='pkg';

    const swiperId = 'sw_'+p.id + '_' + Math.random().toString(36).slice(2,6);
    const imgs = p.images && p.images.length ? p.images : ['https://via.placeholder.com/800x500?text=Sem+imagem'];

    const swiperHtml = `
      <div class="swiper ${swiperId} pacoteSwiper">
        <div class="swiper-wrapper">
          ${imgs.map(src=>`<div class="swiper-slide"><img src="${src}" alt="${p.title}"></div>`).join('')}
        </div>
        <div class="swiper-pagination"></div>
      </div>
    `;

    card.innerHTML = swiperHtml + `
      <div class="pkg-content">
        <div>
          <h3>${escapeHtml(p.title)}</h3>
          <div class="price">${p.price ? money(p.price) : 'Valor variável'}</div>
          <div class="etiquetas">${(p.tags||[]).map(t=>`<span class="etiqueta">${escapeHtml(t)}</span>`).join('')}</div>
          <p style="margin:8px 0;color:var(--muted);font-size:14px">${escapeHtml(p.desc)}</p>
        </div>
        <div>
          ${p.type === 'venda' ? (`<a class="cta ${p.available? '':'indisponivel'}" data-id="${p.id}" ${p.available? '':'aria-disabled="true"'}>${p.available? 'Comprar pelo WhatsApp':'Indisponível'}</a>`) : (`<a class="cta ${p.available? '':'indisponivel'}" data-id="${p.id}">${p.available? 'Reservar / Comprar':'Indisponível'}</a>`) }
        </div>
      </div>
    `;

    if(p.type === 'pacote') pacotesEl.appendChild(card); else vendasEl.appendChild(card);

    // after adding to DOM, init swiper for this card
    setTimeout(()=>{
      try{
        new Swiper('.'+swiperId, {
          loop:true,autoplay:{delay:4000,disableOnInteraction:false},slidesPerView:1,spaceBetween:0,
          pagination:{el:'.'+swiperId+' .swiper-pagination',clickable:true}
        });
      }catch(e){console.warn('swiper err',e)}
    },50);
  });

  // attach click handlers for CTAs
  document.querySelectorAll('.cta').forEach(btn=>{
    btn.addEventListener('click', (ev)=>{
      const id = btn.dataset.id;
      if(!id) return;
      const prod = products.find(x=>x.id===id);
      if(!prod) return;
      if(!prod.available && prod.type==='venda') return alert('Produto indisponível');
      // adicionar ao carrinho local e abrir checkout modal
      addToCart(id,1);
      openCheckout();
    });
  });
}

function escapeHtml(s){ if(!s) return ''; return s.replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":"&#39;"})[c]); }

// Admin actions
qs('#btnToggleAdmin').addEventListener('click', ()=>{
  const panel = qs('#adminPanel'); panel.style.display = panel.style.display === 'none' ? 'block' : 'none';
});

qs('#saveProductBtn').addEventListener('click', async ()=>{
  const name = qs('#pName').value.trim();
  const price = parseFloat(qs('#pPrice').value) || 0;
  const tags = qs('#pTags').value.split(',').map(s=>s.trim()).filter(Boolean);
  const desc = qs('#pDesc').value.trim();
  const files = qs('#pImgs').files;
  if(!name){ alert('Nome obrigatório'); return; }
  const images = [];
  for(const f of files){ images.push(await fileToDataURL(f)); }
  const id = 'p_'+Math.random().toString(36).slice(2,9);
  products.unshift({ id, type: price>0 ? 'venda':'venda', title:name, price, tags, desc, images, available:true });
  localStorage.setItem(STORAGE_PRODUCTS, JSON.stringify(products));
  qs('#pName').value=''; qs('#pPrice').value=''; qs('#pTags').value=''; qs('#pDesc').value=''; qs('#pImgs').value='';
  renderAll();
  alert('Produto salvo localmente!');
});

qs('#clearAllBtn').addEventListener('click', ()=>{
  if(!confirm('Remover TODOS produtos do navegador?')) return;
  products = []; localStorage.setItem(STORAGE_PRODUCTS, JSON.stringify(products)); renderAll();
});

function fileToDataURL(file){ return new Promise((res,rej)=>{ const r = new FileReader(); r.onload = ()=> res(r.result); r.onerror = rej; r.readAsDataURL(file); }); }

// Cart logic
function addToCart(id, qty=1){ cart[id] = (cart[id]||0) + qty; localStorage.setItem(STORAGE_CART, JSON.stringify(cart)); renderCartBadge(); }
function removeFromCart(id){ delete cart[id]; localStorage.setItem(STORAGE_CART, JSON.stringify(cart)); renderCartBadge(); }

function renderCartBadge(){ const count = Object.values(cart).reduce((s,v)=>s+v,0); const b = qs('#cartBadge'); if(count>0){ b.style.display='inline-block'; b.textContent = count; } else b.style.display='none'; }

qs('#cartFab').addEventListener('click', ()=> openCheckout());

function openCheckout(){
  // if user not logged show modal to fill
  if(!currentUser){
    qs('#checkoutModal').style.display = 'flex';
    // try to prefill from storage
    const stored = JSON.parse(localStorage.getItem(STORAGE_USERS) || 'null');
    if(stored){ qs('#cName').value = stored.name || ''; qs('#cEmail').value = stored.email || ''; qs('#cCEP').value = stored.cep || ''; qs('#cCity').value = stored.city || ''; qs('#cAddress').value = stored.address || ''; }
    return;
  }
  // if logged, send directly
  sendOrderToWhatsApp(currentUser);
}

qs('#cancelOrderBtn').addEventListener('click', ()=> qs('#checkoutModal').style.display = 'none');
qs('#confirmOrderBtn').addEventListener('click', ()=>{
  const name = qs('#cName').value.trim(); const email = qs('#cEmail').value.trim(); const cep = qs('#cCEP').value.trim(); const city = qs('#cCity').value.trim(); const addr = qs('#cAddress').value.trim();
  if(!name || !email){ alert('Nome e email são obrigatórios'); return; }
  currentUser = { name, email, cep, city, address:addr };
  localStorage.setItem(STORAGE_USERS, JSON.stringify(currentUser));
  qs('#userArea').textContent = name + ' • ' + email;
  qs('#checkoutModal').style.display = 'none';
  sendOrderToWhatsApp(currentUser);
});

function sendOrderToWhatsApp(user){
  const items = Object.entries(cart).flatMap(([id,qty])=>{
    const p = products.find(x=>x.id===id); if(!p) return []; return [`${p.title} x${qty} — ${money(p.price * qty)}`];
  });
  if(items.length===0){ alert('Carrinho vazio'); return; }
  const subtotal = Object.entries(cart).reduce((s,[id,qty])=>{ const p = products.find(x=>x.id===id); return s + (p? p.price * qty : 0); },0);
  const lines = [
    '*Novo pedido*', '',
    `*Cliente:* ${user.name}`,
    `*Email:* ${user.email}`,
    `*Endereço:* ${user.address || '-'} / ${user.city || '-'} / CEP: ${user.cep || '-'}`, '',
    '*Itens:*', ...items, '',
    `*Total (produtos):* ${money(subtotal)}`,
    '*Observação:* Valor do frete NÃO incluso — combinar via WhatsApp.', '',
    'Por favor confirme disponibilidade e envio.'
  ];
  const encoded = encodeURIComponent(lines.join('
'));
  const url = `https://wa.me/${WA_NUMBER}?text=${encoded}`;
  window.open(url, '_blank');
}

// init
if(currentUser) qs('#userArea').textContent = currentUser.name + ' • ' + currentUser.email; else qs('#userArea').textContent = 'Não logado';
renderAll();

// WhatsApp quick button
qs('#waBtn').href = `https://wa.me/${WA_NUMBER}`;

</script>
</body>
</html>
