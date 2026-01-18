<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>MyDrugs</title>
  <style>
    :root{
      --bg: #0b1020;
      --card: #0f1730;
      --card2: #0b1228;
      --text: #e6e8f2;
      --muted: #aab0c6;
      --accent: #60a5fa;
      --danger: #fb7185;
      --shadow: 0 12px 40px rgba(0,0,0,0.45);
      --border: rgba(255,255,255,0.10);
    }
    *{box-sizing:border-box;}
    body{
      margin:0;
      font-family: Arial, Helvetica, sans-serif;
      background: radial-gradient(1200px 700px at 20% 10%, #1b2a6b, var(--bg) 60%);
      color: var(--text);
    }
    header{
      padding: 36px 20px 18px;
      text-align:center;
      background: linear-gradient(135deg, #2563eb, #1e40af);
    }
    header h1{margin:0; font-size:2.6rem; letter-spacing:1px;}
    header p{margin:10px 0 0; opacity:0.9;}
    nav{
      display:flex;
      justify-content:center;
      gap:18px;
      background: var(--card2);
      padding: 12px;
      border-bottom: 1px solid rgba(255,255,255,0.06);
      position: sticky;
      top:0;
      z-index: 10;
    }
    nav button{
      background: transparent;
      border: none;
      color: var(--text);
      font-weight:700;
      cursor:pointer;
      padding: 10px 14px;
      border-radius: 12px;
    }
    nav button:hover{background: rgba(255,255,255,0.06);}
    nav button.active{background: rgba(255,255,255,0.10);}
    .container{
      max-width: 1100px;
      margin: 34px auto;
      padding: 0 20px 40px;
    }
    .grid{
      display:grid;
      grid-template-columns: 1.3fr .7fr;
      gap: 20px;
      align-items:start;
    }
    .card{
      background: var(--card);
      border-radius: 18px;
      padding: 20px;
      box-shadow: var(--shadow);
    }
    .card h2{margin-top:0;}
    .muted{color:var(--muted); font-size:0.95rem;}
    .menu-grid{
      display:grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 14px;
    }
    .tile{
      background: var(--card2);
      padding: 16px;
      border-radius: 16px;
      cursor:pointer;
      border: 1px solid rgba(255,255,255,0.07);
      transition: transform .12s ease, background .12s ease;
    }
    .tile:hover{transform: translateY(-2px); background: rgba(255,255,255,0.06);}
    .tile .title{font-weight:800; margin-bottom:6px;}
    .tile .desc{color:var(--muted); font-size:0.95rem;}
    .product{
      display:grid;
      grid-template-columns: 1fr 1fr;
      gap: 14px;
    }
    .product .left{
      background: var(--card2);
      border-radius: 16px;
      padding: 16px;
    }
    .product .right{
      background: var(--card2);
      border-radius: 16px;
      padding: 16px;
    }
    .row{display:flex; justify-content:space-between; align-items:center; margin:10px 0;}
    .row label{color:var(--muted); font-size:0.95rem;}
    .input{
      width:100%;
      padding: 10px 12px;
      border-radius: 12px;
      background: rgba(0,0,0,0.22);
      border: 1px solid var(--border);
      color: var(--text);
      font-weight:700;
      outline:none;
    }
    .input:focus{border-color: var(--accent);}
    input[type=range]{width:100%; margin-top:6px;}
    .kassen{
      font-family: monospace;
      font-size:0.95rem;
      line-height:1.5;
      white-space: pre;
      background: rgba(0,0,0,0.25);
      padding: 14px;
      border-radius: 12px;
      border: 1px solid rgba(255,255,255,0.10);
      min-height: 170px;
    }
    .btn{
      display:inline-block;
      padding: 10px 14px;
      border-radius: 12px;
      border: 1px solid rgba(255,255,255,0.12);
      background: rgba(255,255,255,0.06);
      color: var(--text);
      cursor:pointer;
      font-weight:700;
    }
    .btn:hover{background: rgba(255,255,255,0.10);}
    .btn.danger{border-color: rgba(251,113,133,0.35);}
    .btn.primary{border-color: rgba(96,165,250,0.45);}
    footer{
      margin-top: 32px;
      text-align:center;
      padding: 20px;
      background: var(--card2);
      color: var(--muted);
      border-top: 1px solid rgba(255,255,255,0.06);
    }
    @media (max-width: 900px){
      .grid{grid-template-columns: 1fr;}
      .product{grid-template-columns: 1fr;}
    }
  </style>
</head>
<body>

  <header>
    <h1>MyDrugs</h1>
    <p>Willkommen</p>
  </header>

  <nav>
    <button id="menu-home" class="active">Hauptmenü</button>
    <button id="menu-drugs">Drugs</button>
    <button id="menu-support">Support</button>
    <button id="menu-checkout">Zur Kasse</button>
  </nav>

  <div class="container">
    <div id="view-home" class="card">
      <h2>Hauptmenü</h2>
      <div class="menu-grid">
        <div class="tile" data-action="drugs">
          <div class="title">Drugs</div>
          <div class="desc">Wähle deine Droge</div>
        </div>
        <div class="tile" data-action="support">
          <div class="title">Support</div>
          <div class="desc">FAQ & Kontakt</div>
        </div>
      </div>
    </div>

    <div id="view-drugs" class="card" style="display:none;">
      <h2>Drugs</h2>
      <div class="product">
        <div class="left">
          <div class="row">
            <label>Produkt wählen:</label>
            <select id="product-select" class="input" aria-label="Produkt wählen">
              <option value="">-- wählen --</option>
            </select>
          </div>
          <div id="product-list" class="menu-grid"></div>
        </div>
        <div class="right">
          <h3>Produktdetails</h3>
          <div id="product-details" class="muted">Wähle ein Produkt aus der Liste.</div>
          <div id="product-controls" style="display:none; margin-top:12px;">
            <div class="row">
              <label>Preis pro Gramm:</label>
              <div id="price-per-gram"></div>
            </div>
            <div class="row">
              <label>Verfügbar:</label>
              <div id="stock"></div>
            </div>
            <div class="row">
              <label>Gramm auswählen:</label>
              <div id="selected-grams">0</div>
            </div>
            <input id="gram-slider" type="range" min="0" max="0" value="0" oninput="updateSelection()" />
            <div class="row" style="margin-top:10px;">
              <label>Preis (gesamt):</label>
              <div id="total-price">0 €</div>
            </div>
            <button class="btn primary" id="add-to-cart">In den Warenkorb</button>
          </div>
        </div>
      </div>
    </div>

    <div id="view-support" class="card" style="display:none;">
      <h2>Support</h2>
      <p class="muted">Wenn du Fragen hast, schreib uns.</p>
      <div class="card" style="background: var(--card2); margin-top:14px;">
        <h3>FAQ</h3>
        <p><b>Ist Lieferung möglich?</b><br>Ja.</p>
        <p><b>Wie schnell ist die Lieferung?</b><br>Abhängig von der Bestellung.</p>
        <p><b>Kontakt?</b><br>Nutze das Formular.</p>
      </div>
      <div style="margin-top:14px;">
        <h3>Kontaktformular</h3>
        <input id="support-name" class="input" placeholder="Name" />
        <input id="support-email" class="input" placeholder="E-Mail" style="margin-top:10px;" />
        <textarea id="support-msg" class="input" placeholder="Nachricht" style="margin-top:10px; height:120px;"></textarea>
        <button class="btn primary" id="support-send" style="margin-top:10px;">Senden</button>
      </div>
    </div>

    <div id="view-checkout" class="card" style="display:none;">
      <h2>Zur Kasse</h2>
      <div class="grid">
        <div class="card" style="background: var(--card2);">
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

        <div class="card" style="background: var(--card2);">
          <h3>Zusammenfassung</h3>
          <div id="checkout-summary" class="muted">Bitte bestätige zuerst deine Adresse.</div>
          <button class="btn" id="checkout-pay" style="margin-top:12px;" disabled>Kauf bestätigen</button>
        </div>
      </div>
    </div>

    <div id="view-thanks" class="card" style="display:none;">
      <h2>Danke</h2>
      <p id="thanks-text" class="muted"></p>
      <p id="order-id" class="muted"></p>
      <p id="tracking" class="muted"></p>
      <button class="btn" id="thanks-home">Zurück zum Start</button>
      <button class="btn primary" id="download-receipt" style="margin-left:10px;">Rechnung herunterladen (PDF)</button>
    </div>

    <div class="card" style="margin-top:20px;">
      <h2>Kassenbon</h2>
      <div id="receipt" class="kassen">🧾 MyDrugs Receipt

(noch leer)</div>
      <div style="margin-top:10px; display:flex; gap:10px; flex-wrap:wrap;">
        <button class="btn danger" id="clear-cart">Warenkorb leeren</button>
        <button class="btn" id="copy-receipt">Kassenbon kopieren</button>
      </div>
    </div>

  </div>

  <footer>
    MyDrugs • 2026
  </footer>

  <script>
    const products = [
      { id: 'weed', name: 'Weed', price: 20, stock: 15 },
      { id: 'hash', name: 'Hashish', price: 25, stock: 12 },
      { id: 'ecstasy', name: 'Ecstasy', price: 30, stock: 8 },
      { id: 'kokain', name: 'Kokain', price: 45, stock: 10 },
      { id: 'meth', name: 'Meth (Main)', price: 60, stock: 10 },
      { id: 'heroin', name: 'Heroin', price: 50, stock: 6 }
    ];

    let cart = {};
    let selectedProduct = null;

    let lastOrder = null; // speichert die letzte Bestellung

    function setActiveButton(id){
      document.querySelectorAll('nav button').forEach(b=>b.classList.remove('active'));
      document.getElementById(id).classList.add('active');
    }

    function showHome(){
      setActiveButton('menu-home');
      document.getElementById('view-home').style.display='block';
      document.getElementById('view-drugs').style.display='none';
      document.getElementById('view-support').style.display='none';
      document.getElementById('view-checkout').style.display='none';
      document.getElementById('view-thanks').style.display='none';
    }

    function showDrugs(){
      setActiveButton('menu-drugs');
      document.getElementById('view-home').style.display='none';
      document.getElementById('view-drugs').style.display='block';
      document.getElementById('view-support').style.display='none';
      document.getElementById('view-checkout').style.display='none';
      document.getElementById('view-thanks').style.display='none';
      renderProductList();
      populateSelect();
    }

    function showSupport(){
      setActiveButton('menu-support');
      document.getElementById('view-home').style.display='none';
      document.getElementById('view-drugs').style.display='none';
      document.getElementById('view-support').style.display='block';
      document.getElementById('view-checkout').style.display='none';
      document.getElementById('view-thanks').style.display='none';
    }

    function showCheckout(){
      setActiveButton('menu-checkout');
      document.getElementById('view-home').style.display='none';
      document.getElementById('view-drugs').style.display='none';
      document.getElementById('view-support').style.display='none';
      document.getElementById('view-checkout').style.display='block';
      document.getElementById('view-thanks').style.display='none';
      renderCheckoutCart();
      renderCheckoutSummary();
    }

    function showThanks(){
      document.querySelectorAll('nav button').forEach(b=>b.classList.remove('active'));
      document.getElementById('view-home').style.display='none';
      document.getElementById('view-drugs').style.display='none';
      document.getElementById('view-support').style.display='none';
      document.getElementById('view-checkout').style.display='none';
      document.getElementById('view-thanks').style.display='block';
    }

    function renderProductList(){
      const list = document.getElementById('product-list');
      list.innerHTML='';
      products.forEach(p=>{
        const tile = document.createElement('div');
        tile.className='tile';
        tile.innerHTML = `<div class="title">${p.name}</div><div class="desc">${p.price}€/g • noch ${p.stock}g</div>`;
        tile.addEventListener('click', ()=>selectProduct(p.id));
        list.appendChild(tile);
      });
    }

    function populateSelect(){
      const select = document.getElementById('product-select');
      select.innerHTML = '<option value="">-- wählen --</option>';
      products.forEach(p=>{
        const opt = document.createElement('option');
        opt.value = p.id;
        opt.textContent = `${p.name} (${p.stock}g)`;
        select.appendChild(opt);
      });
    }

    function selectProduct(id){
      if(!id) return;
      selectedProduct = products.find(p=>p.id===id);
      document.getElementById('product-select').value = id;
      document.getElementById('product-details').innerHTML = `<b>${selectedProduct.name}</b><br><span class="muted">Wähle Gramm (max ${selectedProduct.stock})</span>`;
      document.getElementById('product-controls').style.display='block';
      const slider = document.getElementById('gram-slider');
      slider.max = selectedProduct.stock;
      slider.value = 0;
      updateSelection();
    }

    function updateSelection(){
      const slider = document.getElementById('gram-slider');
      const grams = parseInt(slider.value, 10) || 0;
      if(!selectedProduct){
        document.getElementById('selected-grams').innerText = '0';
        document.getElementById('total-price').innerText = '0 €';
        return;
      }
      document.getElementById('selected-grams').innerText = grams;
      const total = grams * selectedProduct.price;
      document.getElementById('total-price').innerText = total + ' €';
    }

    function addToCart(){
      const grams = parseInt(document.getElementById('gram-slider').value, 10) || 0;
      if(!selectedProduct || grams<=0) return;
      if(!cart[selectedProduct.id]) cart[selectedProduct.id]=0;
      const newTotal = cart[selectedProduct.id] + grams;
      if(newTotal > selectedProduct.stock){
        alert('Maximaler Bestand erreicht.');
        return;
      }
      cart[selectedProduct.id] = newTotal;
      renderReceipt();
    }

    function renderReceipt(){
      let text = '🧾 MyDrugs Receipt\\n\\n';
      let total = 0;
      const entries = Object.entries(cart);
      if(entries.length===0){
        document.getElementById('receipt').innerText = text + '(noch leer)';
        return;
      }
      entries.forEach(([id, grams])=>{
        const p = products.find(x=>x.id===id);
        text += `${grams}× ${p.name}  (${grams}g × ${p.price}€)\\n`;
        total += grams * p.price;
      });
      text += '\\n----------------\\nTotal: ' + total + ' €';
      document.getElementById('receipt').innerText = text;
    }

    function clearCart(){
      cart = {};
      renderReceipt();
    }

    function copyReceipt(){
      const text = document.getElementById('receipt').innerText;
      navigator.clipboard.writeText(text).then(()=>{ alert('Kassenbon kopiert!'); }).catch(()=>{ alert('Kopieren nicht möglich.'); });
    }

    function renderCheckoutCart(){
      const cartDiv = document.getElementById('checkout-cart');
      const entries = Object.entries(cart);
      if(entries.length===0){
        cartDiv.innerText = '(leer)';
        return;
      }
      let text = '';
      entries.forEach(([id, grams])=>{
        const p = products.find(x=>x.id===id);
        text += `${grams}× ${p.name} (${grams}g)\\n`;
      });
      cartDiv.innerText = text;
    }

    function getCartTotalItems(){
      return Object.values(cart).reduce((a,b)=>a+b,0);
    }

    function getCartTotalPrice(){
      let total=0;
      Object.entries(cart).forEach(([id, grams])=>{
        const p = products.find(x=>x.id===id);
        total += grams * p.price;
      });
      return total;
    }

    function renderCheckoutSummary(){
      const summary = document.getElementById('checkout-summary');
      const totalPrice = getCartTotalPrice();
      if(totalPrice===0){
        summary.innerText = 'Warenkorb ist leer.';
        document.getElementById('checkout-pay').disabled = true;
        return;
      }
      summary.innerText = `Gesamt: ${totalPrice} €\\nProdukte: ${getCartTotalItems()}`;
      document.getElementById('checkout-pay').disabled = false;
    }

    function validateCheckoutForm(){
      const email = document.getElementById('addr-email').value.trim();
      const zip = document.getElementById('addr-zip').value.trim();
      const city = document.getElementById('addr-city').value.trim();
      const street = document.getElementById('addr-street').value.trim();
      return email && zip && city && street;
    }

    function checkoutConfirm(){
      if(!validateCheckoutForm()){
        alert('Bitte fülle alle Felder aus.');
        return;
      }
      renderCheckoutSummary();
      document.getElementById('checkout-pay').disabled = false;
    }

    function checkoutPay(){
      if(!validateCheckoutForm()){
        alert('Bitte bestätige zuerst deine Adresse.');
        return;
      }

      const orderId = generateOrderId();
      const days = calculateDeliveryDays();
      const tracking = generateTracking();

      lastOrder = {
        id: orderId,
        days,
        tracking,
        cart: JSON.parse(JSON.stringify(cart)),
        total: getCartTotalPrice()
      };

      document.getElementById('thanks-text').innerText =
        `Das MyDrugs Team sagt danke für Ihren Einkauf. Rechnung und Bestellung kommen in ${days} Werktagen bei Ihnen an.`;
      document.getElementById('order-id').innerText = `Bestellnummer: ${orderId}`;
      document.getElementById('tracking').innerText = `Tracking: ${tracking}`;

      showThanks();
    }

    function calculateDeliveryDays(){
      const items = getCartTotalItems();
      if(items <= 2) return randomInt(1,2);
      if(items <= 5) return randomInt(3,5);
      return randomInt(6,8);
    }

    function randomInt(min,max){
      return Math.floor(Math.random()*(max-min+1))+min;
    }

    function generateOrderId(){
      const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
      let id = 'MD-';
      for(let i=0;i<8;i++) id += chars[Math.floor(Math.random()*chars.length)];
      return id;
    }

    function generateTracking(){
      const steps = ['In Bearbeitung', 'Verpackt', 'Versendet', 'Unterwegs', 'Zustellung'];
      return steps[randomInt(0, steps.length-1)];
    }

    function downloadPDF(){
      if(!lastOrder){
        alert('Keine Bestellung vorhanden.');
        return;
      }

      const receiptText = document.getElementById('receipt').innerText;
      const pdfContent =
        `MyDrugs Rechnung\n\n` +
        `Bestellnummer: ${lastOrder.id}\n` +
        `Gesamt: ${lastOrder.total} €\n` +
        `Tracking: ${lastOrder.tracking}\n\n` +
        receiptText;

      const blob = new Blob([pdfContent], {type: 'application/pdf'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = `Rechnung_${lastOrder.id}.pdf`;
      a.click();
      URL.revokeObjectURL(url);
    }

    document.getElementById('menu-home').addEventListener('click', showHome);
    document.getElementById('menu-drugs').addEventListener('click', showDrugs);
    document.getElementById('menu-support').addEventListener('click', showSupport);
    document.getElementById('menu-checkout').addEventListener('click', showCheckout);

    document.getElementById('product-select').addEventListener('change', (e)=>selectProduct(e.target.value));
    document.getElementById('add-to-cart').addEventListener('click', addToCart);
    document.getElementById('clear-cart').addEventListener('click', clearCart);
    document.getElementById('copy-receipt').addEventListener('click', copyReceipt);

    document.getElementById('checkout-confirm').addEventListener('click', checkoutConfirm);
    document.getElementById('checkout-pay').addEventListener('click', checkoutPay);

    document.getElementById('support-send').addEventListener('click', ()=>{
      alert('Nachricht gesendet.');
      document.getElementById('support-name').value='';
      document.getElementById('support-email').value='';
      document.getElementById('support-msg').value='';
    });

    document.getElementById('thanks-home').addEventListener('click', showHome);
    document.getElementById('download-receipt').addEventListener('click', downloadPDF);

    // initial
    showHome();
    renderReceipt();
  </script>

</body>
</html>
