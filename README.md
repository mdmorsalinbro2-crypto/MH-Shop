
<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#111827">
<title>MH Store | Fashion Shop</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#f8fafc;color:#111827}
header{background:#111827;color:white;padding:16px;position:sticky;top:0;z-index:5}
.nav{display:flex;justify-content:space-between;align-items:center;gap:10px;flex-wrap:wrap}
.logo{font-size:24px;font-weight:bold;color:#fbbf24}
button{border:0;border-radius:8px;padding:11px 14px;cursor:pointer;font-weight:bold}
.nav button{background:#fbbf24;color:#111827}
.hero{padding:30px 18px;text-align:center;background:#e5e7eb}
.hero h1{font-size:32px;margin:0 0 10px}
.hero p{color:#4b5563}
.search{display:block;width:90%;max-width:500px;margin:18px auto;padding:14px;border:1px solid #cbd5e1;border-radius:10px;font-size:16px}
h2{text-align:center;margin:25px 0 15px}
.products{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px;padding:12px;max-width:1000px;margin:auto}
.card{background:white;border-radius:12px;overflow:hidden;box-shadow:0 2px 8px #0001}
.card img{width:100%;height:175px;object-fit:cover;background:#e5e7eb}
.info{padding:12px}
.info h3{margin:0 0 8px;font-size:16px}
.price{font-weight:bold;color:#047857;margin:8px 0}
.add{width:100%;background:#111827;color:white}
section.panel{background:white;margin:20px 12px;padding:16px;border-radius:12px}
.line{display:flex;justify-content:space-between;align-items:center;gap:10px;padding:10px 0;border-bottom:1px solid #eee}
.line button{padding:7px 10px;background:#e5e7eb}
.action{width:100%;margin-top:10px;background:#16a34a;color:white}
.secondary{width:100%;margin-top:8px;background:#e5e7eb;color:#111827}
input,select{font-size:16px;padding:12px;border:1px solid #cbd5e1;border-radius:8px;width:100%;margin:6px 0}
footer{text-align:center;padding:24px;background:#111827;color:white;margin-top:30px}
small{color:#64748b}
@media(min-width:650px){.products{grid-template-columns:repeat(4,minmax(0,1fr))}.card img{height:220px}}
</style>
</head>
<body>

<header>
 <div class="nav">
  <div class="logo">MH STORE</div>
  <div>
   <button onclick="showCart()">🛒 Cart (<span id="count">0</span>)</button>
   <button onclick="showLogin()">Login</button>
  </div>
 </div>
</header>

<div class="hero">
 <h1>Welcome to MH Store</h1>
 <p>আপনার পছন্দের পোশাক কিনুন সহজেই!</p>
 <strong>Fashion • Style • Comfort</strong>
</div>

<input class="search" id="search" placeholder="পোশাকের নাম লিখে খুঁজুন..."
 oninput="renderProducts()">

<h2>Our Products / আমাদের পোশাক</h2>
<div class="products" id="products"></div>

<section class="panel" id="cartPanel" hidden>
 <h2>আপনার Shopping Cart</h2>
 <div id="cartItems"></div>
 <h3 id="total">মোট: ৳0</h3>
 <label for="customer">আপনার নাম</label>
 <input id="customer" placeholder="আপনার নাম লিখুন">
 <label for="phone">মোবাইল নম্বর</label>
 <input id="phone" type="tel" placeholder="01XXXXXXXXX">
 <label for="address">ডেলিভারির ঠিকানা</label>
 <input id="address" placeholder="গ্রাম/এলাকা, থানা, জেলা">
 <button class="action" onclick="orderWhatsApp()">WhatsApp-এ অর্ডার করুন</button>
 <button class="secondary" onclick="hideCart()">বন্ধ করুন</button>
</section>

<section class="panel" id="loginPanel" hidden>
 <h2>Customer Login (Demo)</h2>
 <p>এই ডেমোতে আপনার নাম শুধু এই ব্রাউজারে রাখা হবে। এটি নিরাপদ অ্যাকাউন্ট নয়।</p>
 <input id="loginName" placeholder="আপনার নাম">
 <button class="action" onclick="demoLogin()">Continue</button>
 <button class="secondary" onclick="demoLogout()">Logout</button>
 <p id="loginStatus"></p>
 <button class="secondary" onclick="hideLogin()">বন্ধ করুন</button>
</section>

<footer>
 <h3>MH STORE</h3>
 <p>আপনার বিশ্বস্ত অনলাইন ফ্যাশন শপ</p>
 <small>অর্ডার নিশ্চিত করার আগে পণ্যের দাম ও ডেলিভারি খরচ যাচাই করুন।</small>
</footer>

<script>
const products = [
 {id:1,name:"Classic T-Shirt",price:350,
 img:"https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=600"},
 {id:2,name:"Casual Shirt",price:650,
 img:"https://images.unsplash.com/photo-1596755094514-f87e34085b2c?w=600"},
 {id:3,name:"Fashion Hoodie",price:850,
 img:"https://images.unsplash.com/photo-1556821840-3a63f95609a7?w=600"},
 {id:4,name:"Denim Jacket",price:1200,
 img:"https://images.unsplash.com/photo-1543076447-215ad9ba6923?w=600"},
 {id:5,name:"White T-Shirt",price:400,
 img:"https://images.unsplash.com/photo-1503341504253-dff4815485f1?w=600"},
 {id:6,name:"Summer Outfit",price:750,
 img:"https://images.unsplash.com/photo-1483985988355-763728e1935b?w=600"},
 {id:7,name:"Black Shirt",price:600,
 img:"https://images.unsplash.com/photo-1603252109303-2751441dd157?w=600"},
 {id:8,name:"Streetwear",price:900,
 img:"https://images.unsplash.com/photo-1523398002811-999ca8dec234?w=600"}
];

let cart = JSON.parse(localStorage.getItem("mhCart") || "{}");

function saveCart(){
 localStorage.setItem("mhCart",JSON.stringify(cart));
 document.getElementById("count").textContent =
 Object.values(cart).reduce((a,b)=>a+b,0);
}

function renderProducts(){
 const q=document.getElementById("search").value.toLowerCase();
 const list=products.filter(p=>p.name.toLowerCase().includes(q));
 document.getElementById("products").innerHTML=list.map(p=>`
 <article class="card">
  <img src="${p.img}" alt="${p.name}" loading="lazy"
   onerror="this.src='https://placehold.co/400x400?text=MH+Store'">
  <div class="info">
   <h3>${p.name}</h3>
   <div class="price">৳${p.price}</div>
   <button class="add" onclick="addCart(${p.id})">Add to Cart</button>
  </div>
 </article>`).join("");
 if(!list.length) document.getElementById("products").innerHTML="কোনো পণ্য পাওয়া যায়নি।";
}

function addCart(id){
 cart[id]=(cart[id]||0)+1;
 saveCart();
 alert("পণ্য Cart-এ যোগ হয়েছে!");
}

function showCart(){
 document.getElementById("cartPanel").hidden=false;
 document.getElementById("loginPanel").hidden=true;
 renderCart();
 document.getElementById("cartPanel").scrollIntoView({behavior:"smooth"});
}

function hideCart(){document.getElementById("cartPanel").hidden=true}

function renderCart(){
 let html="",total=0;
 products.forEach(p=>{
  const qty=cart[p.id]||0;
  if(qty){
   total+=p.price*qty;
   html+=`<div class="line">
    <span>${p.name}<br>৳${p.price} × ${qty}</span>
    <span>
     <button onclick="changeQty(${p.id},-1)">−</button>
     ${qty}
     <button onclick="changeQty(${p.id},1)">+</button>
    </span>
   </div>`;
  }
 });
 document.getElementById("cartItems").innerHTML=html||"আপনার Cart খালি।";
 document.getElementById("total").textContent="মোট: ৳"+total;
}

function changeQty(id,change){
 cart[id]=(cart[id]||0)+change;
 if(cart[id]<=0)delete cart[id];
 saveCart();renderCart();
}

function orderWhatsApp(){
 const name=document.getElementById("customer").value.trim();
 const phone=document.getElementById("phone").value.trim();
 const address=document.getElementById("address").value.trim();
 const items=products.filter(p=>cart[p.id]);
 if(!items.length){alert("প্রথমে Cart-এ পণ্য যোগ করুন।");return}
 if(!name||!phone||!address){
  alert("নাম, মোবাইল নম্বর ও ঠিকানা লিখুন।");return;
 }
 let msg="MH STORE - NEW ORDER%0A";
 msg+="নাম: "+encodeURIComponent(name)+"%0A";
 msg+="ফোন: "+encodeURIComponent(phone)+"%0A";
 msg+="ঠিকানা: "+encodeURIComponent(address)+"%0A%0A";
 let total=0;
 items.forEach(p=>{
  const qty=cart[p.id];
  total+=p.price*qty;
  msg+=encodeURIComponent(p.name+" x "+qty+" = ৳"+(p.price*qty))+"%0A";
 });
 msg+="%0Aমোট পণ্যমূল্য: ৳"+total;
 msg+="%0Aডেলিভারি চার্জ আলাদাভাবে নিশ্চিত করুন।";
 // নিজের WhatsApp নম্বর বসান; দেশের কোড 880, শুরুতে 0 দেবেন না।
 const whatsappNumber="8801XXXXXXXXX";
 if(whatsappNumber.includes("X")){
  alert("প্রথমে কোডে নিজের WhatsApp নম্বর বসান।");
  return;
 }
 window.open("https://wa.me/"+whatsappNumber+"?text="+msg,"_blank");
}

function showLogin(){
 document.getElementById("loginPanel").hidden=false;
 document.getElementById("cartPanel").hidden=true;
 document.getElementById("loginPanel").scrollIntoView({behavior:"smooth"});
}
function hideLogin(){document.getElementById("loginPanel").hidden=true}

function demoLogin(){
 const name=document.getElementById("loginName").value.trim();
 if(!name){alert("আপনার নাম লিখুন।");return}
 localStorage.setItem("mhDemoName",name);
 document.getElementById("loginStatus").textContent="স্বাগতম, "+name+"!";
}
function demoLogout(){
 localStorage.removeItem("mhDemoName");
 document.getElementById("loginStatus").textContent="আপনি Logout করেছেন।";
}

const savedName=localStorage.getItem("mhDemoName");
if(savedName){
 document.getElementById("loginName").value=savedName;
 document.getElementById("loginStatus").textContent="স্বাগতম, "+savedName+"!";
}
renderProducts();
saveCart();
</script>
</body>
</html>
