<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>MyDrugs</title>
  <style>
    :root{
      --bg:#0b1020;--card:#0f1730;--card2:#0b1228;--text:#e6e8f2;--muted:#aab0c6;--accent:#60a5fa;--shadow:0 12px 40px rgba(0,0,0,.45);--border:rgba(255,255,255,.1)
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:Arial,Helvetica,sans-serif;background:radial-gradient(1200px 700px at 20% 10%,#1b2a6b,var(--bg) 60%);color:var(--text)}
    header{padding:36px 20px 18px;text-align:center;background:linear-gradient(135deg,#2563eb,#1e40af)}
    header h1{margin:0;font-size:2.6rem;letter-spacing:1px}
    header p{margin:10px 0 0;opacity:.9}
    nav{display:flex;justify-content:center;gap:18px;background:var(--card2);padding:12px;border-bottom:1px solid rgba(255,255,255,.06);position:sticky;top:0;z-index:10}
    nav button{background:transparent;border:none;color:var(--text);font-weight:700;cursor:pointer;padding:10px 14px;border-radius:12px}
    nav button:hover{background:rgba(255,255,255,.06)}
    nav button.active{background:rgba(255,255,255,.1)}
    .container{max-width:1100px;margin:34px auto;padding:0 20px 40px}
    .grid{display:grid;grid-template-columns:1.3fr .7fr;gap:20px;align-items:start}
    .card{background:var(--card);border-radius:18px;padding:20px;box-shadow:var(--shadow)}
    .card h2{margin-top:0}
    .muted{color:var(--muted);font-size:.95rem}
    .menu-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:14px}
    .tile{background:var(--card2);padding:16px;border-radius:16px;cursor:pointer;border:1px solid rgba(255,255,255,.07);transition:transform .12s ease,background .12s ease}
    .tile:hover{transform:translateY(-2px);background:rgba(255,255,255,.06)}
    .tile .title{font-weight:800;margin-bottom:6px}
    .tile .desc{color:var(--muted);font-size:.95rem}
    .product{display:grid;grid-template-columns:1fr 1fr;gap:14px}
    .product .left,.product .right{background:var(--card2);border-radius:16px;padding:16px}
    .row{display:flex;justify-content:space-between;align-items:center;margin:10px 0}
    .row label{color:var(--muted);font-size:.95rem}
    .input{width:100%;padding:10px 12px;border-radius:12px;background:rgba(0,0,0,.22);border:1px solid var(--border);color:var(--text);font-weight:700;outline:none}
    .input:focus{border-color:var(--accent)}
    input[type=range]{width:100%;margin-top:6px}
    .kassen{font-family:monospace;font-size:.95rem;line-height:1.5;white-space:pre;background:rgba(0,0,0,.25);padding:14px;border-radius:12px;border:1px solid rgba(255,255,255,.1);min-height:170px}
    .btn{display:inline-block;padding:10px 14px;border-radius:12px;border:1px solid rgba(255,255,255,.12);background:rgba(255,255,255,.06);color:var(--text);cursor:pointer;font-weight:700}
    .btn:hover{background:rgba(255,255,255,.1)}
    .btn.primary{border-color:rgba(96,165,250,.45)}
    .btn.danger{border-color:rgba(251,113,133,.35)}
    footer{margin-top:32px;text-align:center;padding:20px;background:var(--card2);color:var(--muted);border-top:1px solid rgba(255,255,255,.06)}
    @media(max-width:900px){.grid,.product{grid-template-columns:1fr}}
  </style>
</head>
<body>
<header><h1>MyDrugs</h1><p>Willkommen</p></header>
<nav>
  <button id="menu-home" class="active">Hauptmenü</button>
  <button id="menu-products">Produkte</button>
  <button id="menu-bundles">Pakete</button>
  <button id="menu-support">Support</button>
  <button id="menu-checkout">Zur Kasse</button>
</nav>

<div class="container">
  <!-- HOME -->
  <div id="view-home" class="card">
    <h2>Hauptmenü</h2>
    <div class="menu-grid">
      <div class="tile" data-action="products"><div class="title">Produkte</div><div class="desc">Einzelne Sorten</div></div>
      <div class="tile" data-action="bundles"><div class="title">Pakete</div><div class="desc">Starter + Mystery Box</div></div>
      <div class="tile" data-action="support"><div class="title">Support</div><div class="desc">FAQ & Wunschliste</div></div>
    </div>
  </div>

  <!-- PRODUCTS -->
  <div id="view-products" class="card" style="display:none;">
    <h2>M-Crystals</h2>
    <div class="product">
      <div class="left">
        <div class="row"><label>Produkt wählen:</label><select id="product-select" class="input"><option value="">-- wählen --</option></select></div>
        <div id="product-list" class="menu-grid"></div>
      </div>
      <div class="right">
        <h3>Produktdetails</h3>
        <div id="product-details" class="muted">Wähle ein Produkt aus der Liste.</div>
        <div id="product-controls" style="display:none;margin-top:12px;">
          <div class="row"><label>Preis pro Gramm:</label><div id="price-per-gram"></div></div>
          <div class="row"><label>Verfügbar:</label><div id="stock"></div></div>
          <div class="row"><label>Gramm auswählen:</label><div id="selected-grams">0</div></div>
          <input id="gram-slider" type="range" min="0" max="0" value="0" />
          <div class="row" style="margin-top:10px;"><label>Preis (gesamt):</label><div id="total-price">0 €</div></div>
          <button class="btn primary" id="add-to-cart">In den Warenkorb</button>
        </div>
      </div>
    </div>
  </div>

  <!-- BUNDLES -->
  <div id="view-bundles" class="card" style="display:none;">
    <h2>Pakete</h2>
    <div class="menu-grid">
      <div class="tile" id="bundle-starter">
        <div class="title">Starter Paket</div>
        <div class="desc">5 Sorten • 5g • 320 €</div>
      </div>
      <div class="tile" id="bundle-mystery">
        <div class="title">Mystery Box</div>
        <div class="desc">3 zufällige Sorten • 200 €</div>
      </div>
    </div>
  </div>

  <!-- SUPPORT -->
  <div id="view-support" class="card" style="display:none;">
    <h2>Support</h2>
    <p class="muted">Fragen? Schreib uns.</p>
    <div class="card" style="background:var(--card2);margin-top:14px;"><h3>FAQ</h3><p><b>Lieferung?</b><br>Standard.</p><p><b>Dauer?</b><br>Abhängig von der Bestellung.</p></div>

    <div style="margin-top:14px;">
      <h3>Kontakt</h3>
      <input id="support-name" class="input" placeholder="Name" />
      <input id="support-email" class="input" placeholder="E-Mail" style="margin-top:10px;" />
      <textarea id="support-msg" class="input" placeholder="Nachricht" style="margin-top:10px;height:120px;"></textarea>
      <button class="btn primary" id="support-send" style="margin-top:10px;">Senden</button>
    </div>

    <div style="margin-top:14px;">
      <h3>Wunschliste</h3>
      <input id="wish-text" class="input" placeholder="Schreibe deinen Wunsch..." />
      <button class="btn primary" id="wish-send" style="margin-top:10px;">Wunsch absenden</button>
      <div id="wish-list" class="muted" style="margin-top:10px;white-space:pre-wrap;"></div>
    </div>
  </div>

  <!-- CHECKOUT -->
  <div id="view-checkout" class="card" style="display:none;">
    <h2>Zur Kasse</h2>
    <div class="grid">
      <div class="card" style="background:var(--card2);">
        <h3>Warenkorb</h3>
        <div id="checkout-cart" class="muted">(leer)</div>
        <div style="margin-top:14px;">
          <h3>Adresse</h3>
          <input id="addr-email" class="input" placeholder="E-Mail" />
          <input id="addr-zip" class="input" placeholder="Postleitzahl" style="margin-top:10px;" />
          <input id="addr-city" class="input" placeholder="Stadt" style="margin-top:10px;" />
          <input id="addr-street" class="input" placeholder="Straße + Hausnummer" style="margin-top:10px;" />
          <button class="btn primary" id="checkout-confirm" style="margin-top:12px;">Bestätigen</button>
        </div>
      </div>
      <div class="card" style="background:var(--card2);">
        <h3>Zusammenfassung</h3>
        <div id="checkout-summary" class="muted">Bitte bestätige zuerst deine Adresse.</div>
        <button class="btn" id="checkout-pay" style="margin-top:12px;" disabled>Kauf bestätigen</button>
      </div>
    </div>
  </div>

  <!-- THANKS -->
  <div id="view-thanks" class="card" style="display:none;">
    <h2>Danke</h2>
    <p id="thanks-text" class="muted"></p>
    <p id="order-id" class="muted"></p>
    <p id="tracking" class="muted"></p>
    <button class="btn" id="thanks-home">Zurück zum Start</button>
  </div>

  <!-- RECEIPT -->
  <div class="card" style="margin-top:20px;">
    <h2>Kassenbon</h2>
    <div id="receipt" class="kassen">🧾 MyDrugs Receipt\n\n(noch leer)</div>
    <div style="margin-top:10px;display:flex;gap:10px;flex-wrap:wrap;">
      <button class="btn danger" id="clear-cart">Warenkorb leeren</button>
      <button class="btn" id="copy-receipt">Kassenbon kopieren</button>
    </div>
  </div>
</div>

<footer>MyDrugs • 2026</footer>

<script>
  const products=[
    {id:'mcrystal-classic',name:'M-Crystals – Classic',price:65,stock:20},
    {id:'mcrystal-blue',name:'M-Crystals – Blue Ice',price:70,stock:12},
    {id:'mcrystal-cherry',name:'M-Crystals – Cherry Rush',price:70,stock:10},
    {id:'mcrystal-lemon',name:'M-Crystals – Lemon Spark',price:75,stock:14},
    {id:'mcrystal-mint',name:'M-Crystals – Mint Freeze',price:75,stock:9},
    {id:'mcrystal-grape',name:'M-Crystals – Grape Wave',price:75,stock:11},
    {id:'mcrystal-apple',name:'M-Crystals – Green Apple',price:80,stock:8},
    {id:'mcrystal-vanilla',name:'M-Crystals – Vanilla Frost',price:80,stock:6},
    {id:'mcrystal-monster',name:'M-Crystals – Monster Energy White',price:80,stock:7}
  ];

  let cart={},selectedProduct=null;
  let wishes=[];

  const qs=id=>document.getElementById(id);

  function setActive(id){
    document.querySelectorAll('nav button').forEach(b=>b.classList.remove('active'));
    qs(id).classList.add('active');
  }

  function show(v){
    ['home','products','bundles','support','checkout','thanks'].forEach(x=>qs('view-'+x).style.display='none');
    qs('view-'+v).style.display='block';
  }

  function showHome(){setActive('menu-home');show('home')}
  function showProducts(){setActive('menu-products');show('products');renderProducts();populateSelect()}
  function showBundles(){setActive('menu-bundles');show('bundles');renderBundles()}
  function showSupport(){setActive('menu-support');show('support');renderWishes()}
  function showCheckout(){setActive('menu-checkout');show('checkout');renderCheckout()}
  function showThanks(){document.querySelectorAll('nav button').forEach(b=>b.classList.remove('active'));show('thanks')}

  function renderProducts(){
    const list=qs('product-list');
    list.innerHTML='';
    products.forEach(p=>{
      const t=document.createElement('div');
      t.className='tile';
      t.innerHTML=`<div class=title>${p.name}</div><div class=desc>${p.price}€/g • ${p.stock}g</div>`;
      t.onclick=()=>selectProduct(p.id);
      list.appendChild(t);
    });
  }

  function populateSelect(){
    const s=qs('product-select');
    s.innerHTML='<option value=\"\">-- wählen --</option>';
    products.forEach(p=>{
      const o=document.createElement('option');
      o.value=p.id;
      o.textContent=`${p.name} (${p.stock}g)`;
      s.appendChild(o);
    });
  }

  function selectProduct(id){
    selectedProduct=products.find(p=>p.id===id);
    qs('product-select').value=id;
    qs('product-details').innerHTML=`<b>${selectedProduct.name}</b>`;
    qs('product-controls').style.display='block';
    qs('price-per-gram').innerText=selectedProduct.price+' €';
    qs('stock').innerText=selectedProduct.stock+' g';
    const sl=qs('gram-slider');
    sl.max=selectedProduct.stock;
    sl.value=0;
    updateSelection();
  }

  function updateSelection(){
    const g=+qs('gram-slider').value||0;
    qs('selected-grams').innerText=g;
    qs('total-price').innerText=(selectedProduct?g*selectedProduct.price:0)+' €';
  }

  function addToCart(){
    const g=+qs('gram-slider').value||0;
    if(!selectedProduct||g<=0) return;
    cart[selectedProduct.id]=(cart[selectedProduct.id]||0)+g;
    renderReceipt();
  }

  function renderReceipt(){
    let t='🧾 MyDrugs Receipt\\n\\n';
    let tot=0;
    const e=Object.entries(cart);
    if(!e.length){
      qs('receipt').innerText=t+'(noch leer)';
      return;
    }
    e.forEach(([id,g])=>{
      const p=products.find(x=>x.id===id);
      t+=`${g}× ${p.name} (${g}g × ${p.price}€)\\n`;
      tot+=g*p.price;
    });
    t+=`\\n----------------\\nTotal: ${tot} €`;
    qs('receipt').innerText=t;
  }

  function renderCheckout(){
    const e=Object.entries(cart);
    qs('checkout-cart').innerText=e.length?e.map(([id,g])=>`${g}× ${products.find(p=>p.id===id).name}`).join('\\n'):'(leer)';
    qs('checkout-summary').innerText=e.length?`Gesamt: ${Object.entries(cart).reduce((s,[id,g])=>s+g*products.find(p=>p.id===id).price,0)} €`:'Warenkorb ist leer.';
    qs('checkout-pay').disabled=!e.length;
  }

  function checkoutConfirm(){
    if(!qs('addr-email').value||!qs('addr-zip').value||!qs('addr-city').value||!qs('addr-street').value){
      alert('Bitte alles ausfüllen');
      return;
    }
    qs('checkout-pay').disabled=false;
  }

  function checkoutPay(){
    const days=Math.max(1,Math.ceil(Object.values(cart).reduce((a,b)=>a+b,0)/2));
    qs('thanks-text').innerText=`Das MyDrugs Team sagt danke für Ihren Einkauf. Rechnung und Bestellung kommen in ${days} Werktagen bei Ihnen an.`;
    qs('order-id').innerText='Bestellnummer: MD-'+Math.random().toString(36).slice(2,10).toUpperCase();
    qs('tracking').innerText='Tracking: In Bearbeitung';
    showThanks();
  }

  // Bundles
  function renderBundles(){
    // disable bundles if not enough stock
    const starterOk = products.every(p=>p.stock>=1);
    const mysteryOk = products.filter(p=>p.stock>=1).length>=3;

    qs('bundle-starter').style.opacity = starterOk ? '1' : '0.5';
    qs('bundle-starter').style.pointerEvents = starterOk ? 'auto' : 'none';
    qs('bundle-mystery').style.opacity = mysteryOk ? '1' : '0.5';
    qs('bundle-mystery').style.pointerEvents = mysteryOk ? 'auto' : 'none';
  }

  function addStarterPackage(){
    // remove 1g of each product
    products.forEach(p=>p.stock-=1);
    cart['bundle-starter']=(cart['bundle-starter']||0)+1;
    renderReceipt();
  }

  function addMysteryBox(){
    const available = products.filter(p=>p.stock>=1);
    if(available.length<3) return;
    // choose 3 random unique products
    const chosen=[];
    while(chosen.length<3){
      const pick = available[Math.floor(Math.random()*available.length)];
      if(!chosen.includes(pick)) chosen.push(pick);
    }
    chosen.forEach(p=>p.stock-=1);
    cart['bundle-mystery']=(cart['bundle-mystery']||0)+1;
    renderReceipt();
  }

  function renderReceipt(){
    let t='🧾 MyDrugs Receipt\\n\\n';
    let tot=0;
    const e=Object.entries(cart);
    if(!e.length){
      qs('receipt').innerText=t+'(noch leer)';
      return;
    }
    e.forEach(([id,q])=>{
      if(id==='bundle-starter'){
        t+=`${q}× Starter Paket (5 Sorten)\\n`;
        tot+=q*320;
      } else if(id==='bundle-mystery'){
        t+=`${q}× Mystery Box (3 Sorten)\\n`;
        tot+=q*200;
      } else {
        const p=products.find(x=>x.id===id);
        t+=`${q}× ${p.name} (${q}g × ${p.price}€)\\n`;
        tot+=q*p.price;
      }
    });
    t+=`\\n----------------\\nTotal: ${tot} €`;
    qs('receipt').innerText=t;
  }

  // Wishes
  function renderWishes(){
    qs('wish-list').innerText = wishes.length ? wishes.map((w,i)=>`${i+1}. ${w}`).join('\\n') : '(noch keine Wünsche)';
  }

  function addWish(){
    const text = qs('wish-text').value.trim();
    if(!text) return;
    wishes.unshift(text);
    if(wishes.length>10) wishes.pop();
    qs('wish-text').value='';
    renderWishes();
  }

  // Events
  qs('menu-home').onclick=showHome;
  qs('menu-products').onclick=showProducts;
  qs('menu-bundles').onclick=showBundles;
  qs('menu-support').onclick=showSupport;
  qs('menu-checkout').onclick=showCheckout;

  qs('product-select').onchange=e=>selectProduct(e.target.value);
  qs('gram-slider').oninput=updateSelection;
  qs('add-to-cart').onclick=addToCart;

  qs('bundle-starter').onclick=addStarterPackage;
  qs('bundle-mystery').onclick=addMysteryBox;

  qs('clear-cart').onclick=()=>{
    cart={};
    renderReceipt();
  };
  qs('copy-receipt').onclick=()=>navigator.clipboard.writeText(qs('receipt').innerText);

  qs('checkout-confirm').onclick=checkoutConfirm;
  qs('checkout-pay').onclick=checkoutPay;

  qs('support-send').onclick=()=>{
    alert('Gesendet');
    qs('support-name').value=qs('support-email').value=qs('support-msg').value='';
  };

  qs('wish-send').onclick=addWish;
  qs('thanks-home').onclick=showHome;

  showHome();
  renderReceipt();
</script>
</body>
</html>
