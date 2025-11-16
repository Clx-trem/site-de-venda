<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>CasaRes Play - Loja CLX</title>

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
</style>
</head>
<body>

<header>
  <h1>CasaRes Play</h1>
  <p>Aluguel e venda de pelúcias — diversão garantida nas festas!</p>
</header>

<main>

  <h2 class="fundo-branco">Venda de Pelúcias 🧸</h2>
  <div class="pricing">

    <div class="pkg">
      <div class="swiper pacoteSwiper">
        <div class="swiper-wrapper">
          <div class="swiper-slide"><img src="pelucia10a.jpg" alt="Kit 10 pelúcias - 1"></div>
          <div class="swiper-slide"><img src="pelucia10b.jpg" alt="Kit 10 pelúcias - 2"></div>
        </div>
        <div class="swiper-pagination"></div>
      </div>
      <div class="pkg-content">
        <h3>Kit com 10 Pelúcias</h3>
        <div class="price">R$ 150</div>
        <div class="etiquetas">
          <span class="etiqueta">Entrega Fácil</span>
          <span class="etiqueta">Frete Grátis</span>
        </div>
        <ul>
          <li>10 pelúcias sortidas</li>
          <li>Qualidade premium</li>
          <li>Envio combinado pelo WhatsApp</li>
        </ul>
        <a class="cta" href="https://wa.me/5521990819172?text=Olá! Quero comprar o *Kit com 10 Pelúcias* por R$150." target="_blank">Comprar pelo WhatsApp</a>
      </div>
    </div>

    <div class="pkg">
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
        <a class="cta" href="https://wa.me/5521990819172?text=Olá! Quero comprar o *Kit com 20 Pelúcias* por R$280." target="_blank">Comprar pelo WhatsApp</a>
      </div>
    </div>

  </div>

  <div class="avisos">
    <h3>Informações importantes</h3>
    <p>Tempo de locação: 4 horas. Caso precise de horário estendido ou transporte fora das regiões atendidas, entre em contato.</p>
    <h3>Onde entregamos</h3>
    <p>Paracambi, Seropédica, Japeri e Conrado — frete grátis nessas localidades.</p>
    <h3>Como comprar</h3>
    <ol>
      <li>Clique no botão 'Comprar pelo WhatsApp'.</li>
      <li>Combine o kit e o endereço de entrega.</li>
      <li>Pagamento: na hora da entrega.</li>
    </ol>
  </div>

</main>

<div class="floating-buttons">
  <a href="https://wa.me/5521990819172" target="_blank" class="whatsapp">
    <img src="https://upload.wikimedia.org/wikipedia/commons/6/6b/WhatsApp.svg" alt="WhatsApp">
  </a>
</div>

<footer>
  © CasaRes Play — Aluguel e venda de pelúcias.<br>
  Contato: (21) 99081-9172 — casaresplayfesta@gmail.com
</footer>

<script>
document.querySelectorAll('.pacoteSwiper').forEach((swiperEl)=>{
  new Swiper(swiperEl, {
    loop: true,
    autoplay: { delay: 5000, disableOnInteraction: false },
    slidesPerView: 1,
    spaceBetween: 0,
    pagination: { el: swiperEl.querySelector('.swiper-pagination'), clickable: true }
  });
});
</script>

</body>
</html>
