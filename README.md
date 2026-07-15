<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cafe Four Brothers</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:'Poppins',sans-serif;
}

body{
background:#f4f8fb;
color:#333;
}

header{
background:linear-gradient(rgba(0,0,0,.5),rgba(0,0,0,.5)),
url('https://images.unsplash.com/photo-1507525428034-b723cf961d3e');
background-size:cover;
background-position:center;
height:90vh;
display:flex;
justify-content:center;
align-items:center;
text-align:center;
color:white;
padding:20px;
}

header h1{
font-size:3rem;
margin-bottom:10px;
}

header p{
font-size:1.1rem;
}

.container{
width:90%;
max-width:1200px;
margin:auto;
padding:60px 0;
}

.title{
text-align:center;
margin-bottom:40px;
}

.title h2{
color:#0f3460;
}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:20px;
}

.card{
background:white;
padding:20px;
border-radius:15px;
box-shadow:0 5px 15px rgba(0,0,0,.08);
position:relative;
}

.card h3{
margin-bottom:5px;
}

.card .stock{
font-size:12px;
color:#888;
margin-bottom:8px;
}

.price{
color:#1e88e5;
font-weight:bold;
margin-bottom:10px;
}

button{
background:#1e88e5;
color:white;
border:none;
padding:10px 15px;
border-radius:8px;
cursor:pointer;
font-weight:500;
transition:all 0.3s;
}

button:hover{
background:#1565c0;
transform:scale(1.02);
}

button:disabled{
background:#aaa;
cursor:not-allowed;
transform:none;
}

.cart{
position:fixed;
right:20px;
bottom:20px;
width:340px;
background:white;
padding:20px;
border-radius:15px;
box-shadow:0 5px 20px rgba(0,0,0,.2);
max-height:500px;
overflow:auto;
z-index:999;
}

.cart h3{
margin-bottom:10px;
border-bottom:2px solid #f0f0f0;
padding-bottom:8px;
}

.cart-item{
display:flex;
justify-content:space-between;
align-items:center;
margin-bottom:8px;
font-size:14px;
padding:5px 0;
border-bottom:1px dashed #eee;
}

.cart-item .item-info{
display:flex;
align-items:center;
gap:8px;
}

.cart-item .item-info span{
margin-right:5px;
}

.cart-item .btn-hapus{
background:#ff4757;
color:white;
border:none;
padding:2px 10px;
border-radius:12px;
cursor:pointer;
font-size:12px;
font-weight:bold;
transition:all 0.3s;
}

.cart-item .btn-hapus:hover{
background:#c0392b;
transform:scale(1.05);
}

.cart-total{
margin-top:10px;
padding-top:10px;
border-top:2px solid #f0f0f0;
font-weight:600;
}

.whatsapp{
width:100%;
margin-top:15px;
background:#25D366;
font-weight:bold;
padding:12px;
}

.whatsapp:hover{
background:#1da851;
}

.kosong{
color:#aaa;
text-align:center;
padding:15px 0;
font-style:italic;
}

footer{
background:#0f3460;
color:white;
text-align:center;
padding:20px;
margin-top:60px;
}

/* Responsive Cart */
@media(max-width:768px){
.cart{
width:90%;
right:5%;
bottom:10px;
max-height:400px;
}
header h1{
font-size:2rem;
}
}
</style>
</head>
<body>

<header>
<div>
<h1>Cafe Four Brothers</h1>
<p>Seafood • Cafe • Homestay • Pantai Binasi</p>
</div>
</header>

<div class="container">

<div class="title">
<h2>🍽 Aneka Makanan</h2>
</div>

<div class="grid" id="menuMakanan">
<!-- Makanan akan di-generate oleh JS -->
</div>

<br><br>

<div class="title">
<h2>🥤 Aneka Minuman</h2>
</div>

<div class="grid" id="menuMinuman">
<!-- Minuman akan di-generate oleh JS -->
</div>

</div>

<!-- Keranjang -->
<div class="cart">
<h3>🛒 Keranjang</h3>
<div id="cartItems"></div>
<div class="cart-total">
<p><b>Total Item:</b> <span id="total">0</span></p>
</div>
<button class="whatsapp" onclick="checkoutWA()">
📱 Pesan via WhatsApp
</button>
</div>

<footer>
<p>© 2026 Cafe Four Brothers - Pantai Binasi</p>
</footer>

<script>
// ===== DATA MENU DENGAN STOK =====
const menuData = {
makanan: [
{ nama: "Nasi Goreng", harga: 20000, stok: 10 },
{ nama: "Ayam Penyet", harga: 22000, stok: 8 },
{ nama: "Indomie Kuah", harga: 15000, stok: 12 },
{ nama: "Indomie Goreng", harga: 15000, stok: 12 },
{ nama: "Udang Goreng Tepung", harga: 35000, stok: 5 },
{ nama: "Cumi Goreng Tepung", harga: 35000, stok: 5 },
{ nama: "Ikan Bakar Gambolo", harga: 45000, stok: 4 }
],
minuman: [
{ nama: "Jus Buah Naga", harga: 15000, stok: 7 },
{ nama: "Jus Jeruk", harga: 12000, stok: 8 },
{ nama: "Jus Alpukat", harga: 14000, stok: 6 },
{ nama: "Kelapa Muda", harga: 18000, stok: 5 },
{ nama: "Teh Susu", harga: 10000, stok: 10 },
{ nama: "Teh Manis", harga: 8000, stok: 10 },
{ nama: "Pop Ice", harga: 10000, stok: 8 },
{ nama: "Coca Cola", harga: 12000, stok: 6 },
{ nama: "Fanta", harga: 12000, stok: 6 },
{ nama: "Aqua Botol Menengah", harga: 7000, stok: 15 },
{ nama: "Aqua Botol Besar", harga: 10000, stok: 10 },
{ nama: "Sprite", harga: 12000, stok: 6 },
{ nama: "Milku", harga: 8000, stok: 8 },
{ nama: "Capuccino", harga: 15000, stok: 5 },
{ nama: "Kopi Luwak", harga: 25000, stok: 4 },
{ nama: "Milo", harga: 12000, stok: 7 },
{ nama: "Good Day", harga: 10000, stok: 8 }
]
};

// ===== STATE =====
let cart = {}; // { "Nama Item": jumlah }
let stok = {}; // { "Nama Item": stok_tersisa }

// Inisialisasi stok dari data
function initStok() {
const semuaMenu = [...menuData.makanan, ...menuData.minuman];
semuaMenu.forEach(item => {
stok[item.nama] = item.stok;
});
}
initStok();

// ===== RENDER MENU =====
function renderMenu() {
// Makanan
const containerMakanan = document.getElementById('menuMakanan');
containerMakanan.innerHTML = menuData.makanan.map(item => `
<div class="card">
<h3>${item.nama}</h3>
<div class="stock">📦 Stok: ${stok[item.nama] || 0}</div>
<p class="price">Rp ${item.harga.toLocaleString('id-ID')}</p>
<button onclick="tambahPesanan('${item.nama}')" ${stok[item.nama] <= 0 ? 'disabled' : ''}>
${stok[item.nama] > 0 ? '➕ Tambah' : '❌ Habis'}
</button>
</div>
`).join('');

// Minuman
const containerMinuman = document.getElementById('menuMinuman');
containerMinuman.innerHTML = menuData.minuman.map(item => `
<div class="card">
<h3>${item.nama}</h3>
<div class="stock">📦 Stok: ${stok[item.nama] || 0}</div>
<button onclick="tambahPesanan('${item.nama}')" ${stok[item.nama] <= 0 ? 'disabled' : ''}>
${stok[item.nama] > 0 ? '➕ Tambah' : '❌ Habis'}
</button>
</div>
`).join('');
}

// ===== TAMBAH PESANAN =====
function tambahPesanan(item) {
if (stok[item] <= 0) {
alert('Maaf, stok ' + item + ' habis!');
return;
}

// Kurangi stok
stok[item]--;

// Tambah ke keranjang
if (cart[item]) {
cart[item]++;
} else {
cart[item] = 1;
}

renderCart();
renderMenu(); // update tampilan stok
}

// ===== HAPUS PESANAN =====
function hapusPesanan(item) {
if (!cart[item]) return;

// Kembalikan stok sesuai jumlah yang dihapus
stok[item] += cart[item];

// Hapus dari keranjang
delete cart[item];

renderCart();
renderMenu();
}

// ===== RENDER KERANJANG =====
function renderCart() {
const container = document.getElementById('cartItems');
let html = '';
let total = 0;

const items = Object.keys(cart);

if (items.length === 0) {
html = '<div class="kosong">🛒 Keranjang kosong</div>';
} else {
items.forEach(item => {
total += cart[item];
html += `
<div class="cart-item">
<div class="item-info">
<span>${item}</span>
<span><b>x${cart[item]}</b></span>
</div>
<button class="btn-hapus" onclick="hapusPesanan('${item}')">✕ Hapus</button>
</div>
`;
});
}

container.innerHTML = html;
document.getElementById('total').innerText = total;
}

// ===== CHECKOUT WHATSAPP =====
function checkoutWA() {
const items = Object.keys(cart);
if (items.length === 0) {
alert('🛒 Keranjang masih kosong!');
return;
}

let pesan = "Halo Cafe Four Brothers,%0A%0ASaya ingin memesan:%0A";

items.forEach(item => {
pesan += "- " + item + " x" + cart[item] + "%0A";
});

pesan += "%0AAtas Nama : %0ANomor HP : %0A";

// Reset stok dan keranjang setelah checkout (opsional)
// Bisa dikomentari jika ingin stok tetap berkurang
// for(let item in cart) {
//   stok[item] += cart[item];
// }
// cart = {};
// renderCart();
// renderMenu();

window.open(
"https://wa.me/6282285572953?text=" + pesan,
"_blank"
);
}

// ===== INIT =====
renderMenu();
renderCart();
</script>

</body>
</html>
