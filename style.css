// ===================================================================================
// DATA PRODUK (Tidak ada perubahan)
// ===================================================================================
const products = [
    { id: 1, name: "Celestial Angel", price: 13000, img: "images/1.Celestial Angel.jpg", description: { id: "Gelang dengan tema langit yang memberikan kesan dingin dan menenangkan.", en: "A sky-themed bracelet that gives a cool and calming impression." }},
    { id: 2, name: "Pink Starlight", price: 12000, img: "images/2.Pink Starlight.jpg", description: { id: "Gelang yang memancarkan pesona manis dan galaksi dalam balutan warna pink lembut.", en: "A bracelet that radiates sweet, galactic charm in a soft pink hue." }},
    { id: 3, name: "Fairy Butterfly", price: 16000, img: "images/3.Fairy Butterfly.jpg", description: { id: "Gelang penuh fantasi dengan tema peri dan kupu-kupu!", en: "A fantasy-filled bracelet with a fairy and butterfly theme!" }},
    { id: 4, name: "Botanical Bloom", price: 14000, img: "images/4.Botanical Bloom.jpg", description: { id: "Terinspirasi dari keindahan taman bunga, cocok untuk kamu yang berjiwa bebas.", en: "Inspired by the beauty of a flower garden, perfect for a free spirit." }},
    { id: 5, name: "Berry Garden", price: 15000, img: "images/5.Berry Garden.jpg", description: { id: "Gelang fun dan menyegarkan dengan tema buah-buahan dan taman!", en: "A fun and refreshing bracelet with a fruit and garden theme!" }},
    { id: 6, name: "Golden Harvest", price: 15000, img: "images/6.Golden Harvest.jpg", description: { id: "Gelang elegan dengan nuansa hangat musim gugur dan keemasan.", en: "An elegant bracelet with warm autumn and golden nuances." }},
    { id: 7, name: "White Angelic", price: 16000, img: "images/7.White Agelic.jpg", description: { id: "Gelang monokromatik yang elegan dengan nuansa putih bersih dan perak.", en: "An elegant monochromatic bracelet with clean white and silver nuances." }},
    { id: 8, name: "Lavender Dream", price: 12000, img: "images/8.Lavender Dream.jpg", description: { id: "Gelang cantik yang memancarkan pesona feminim dan elegan.", en: "A beautiful bracelet that exudes feminine and elegant charm." }}
];
const noWhatsApp = "62895320181656";

// ===================================================================================
// FUNGSI UNTUK HALAMAN PRODUK (`produk.html`)
// ===================================================================================
function renderProducts() {
    const productGrid = document.getElementById('all-products-grid'); 
    if (!productGrid) return;
    const currentLang = localStorage.getItem('lang') || 'id';
    productGrid.innerHTML = '';
    products.forEach(product => {
        const productCard = document.createElement('div');
        productCard.className = 'product-card';
        productCard.innerHTML = `
            <img src="${product.img}" alt="${product.name}" />
            <h3>${product.name}</h3>
            <p class="price">Rp ${product.price.toLocaleString('id-ID')}</p>
            <p class="product-description">${product.description[currentLang]}</p> 
            <button onclick="openQuantityModal(${product.id})" class="button" data-lang-key="addToCartBtn">Masukkan ke Keranjang</button>
        `;
        productGrid.appendChild(productCard);
    });
}

// ===================================================================================
// FUNGSI POP-UP (MODAL)
// ===================================================================================
const modal = document.getElementById('quantity-modal');
const modalProductName = document.getElementById('modal-product-name');
const modalProductImg = document.getElementById('modal-product-img');
const modalProductPrice = document.getElementById('modal-product-price');
const modalQuantityInput = document.getElementById('modal-quantity-input');
const modalTotalPrice = document.getElementById('modal-total-price');
const modalAddToCartBtn = document.getElementById('modal-add-to-cart-btn');
const modalQuantityPlus = document.getElementById('modal-quantity-plus');
const modalQuantityMinus = document.getElementById('modal-quantity-minus');
let currentProduct = null;

function openQuantityModal(productId) {
    currentProduct = products.find(p => p.id === productId);
    if (!currentProduct) return;
    modalProductName.textContent = currentProduct.name;
    modalProductImg.src = currentProduct.img;
    modalProductPrice.textContent = `Rp ${currentProduct.price.toLocaleString('id-ID')}`;
    modalQuantityInput.value = 1;
    updateModalTotal();
    modal.style.display = 'block';
    setLanguage(localStorage.getItem('lang') || 'id');
}

function closeQuantityModal() {
    if (modal) modal.style.display = 'none';
    currentProduct = null;
}

function updateModalTotal() {
    if (!currentProduct) return;
    const quantity = parseInt(modalQuantityInput.value) || 1;
    const total = quantity * currentProduct.price;
    modalTotalPrice.textContent = `Rp ${total.toLocaleString('id-ID')}`;
}

if (modal) {
    modalQuantityPlus.onclick = () => { modalQuantityInput.value = parseInt(modalQuantityInput.value) + 1; updateModalTotal(); };
    modalQuantityMinus.onclick = () => { const val = parseInt(modalQuantityInput.value); if (val > 1) { modalQuantityInput.value = val - 1; updateModalTotal(); }};
    modalQuantityInput.oninput = updateModalTotal;
    modalAddToCartBtn.onclick = () => { if (!currentProduct) return; const qty = parseInt(modalQuantityInput.value); if (qty > 0) { addToCart(currentProduct.id, qty); closeQuantityModal(); alert(`${qty} buah ${currentProduct.name} berhasil ditambahkan!`); }};
    window.onclick = function(event) { if (event.target == modal) { closeQuantityModal(); }};
}

// ===================================================================================
// FUNGSI KERANJANG BELANJA
// ===================================================================================
function addToCart(productId, quantity = 1) {
    let cart = JSON.parse(localStorage.getItem('cart')) || [];
    const product = products.find(p => p.id === productId);
    const existingProduct = cart.find(item => item.id === productId);
    if (existingProduct) { existingProduct.quantity += quantity; } 
    else { cart.push({ ...product, quantity: quantity }); }
    localStorage.setItem('cart', JSON.stringify(cart));
    updateCartBadge();
}

function loadCartItems() {
    const cartItemsContainer = document.getElementById('cart-items-container');
    const cartTotalElement = document.getElementById('cart-total');
    if (!cartItemsContainer) return;
    let cart = JSON.parse(localStorage.getItem('cart')) || [];
    cartItemsContainer.innerHTML = '';
    if (cart.length === 0) {
        cartItemsContainer.innerHTML = `<p data-lang-key="emptyCart"></p>`;
        cartTotalElement.innerText = 'Rp 0';
        setLanguage(localStorage.getItem('lang') || 'id'); // Update text "keranjang kosong"
        return;
    }
    let total = 0;
    cart.forEach(item => {
        const cartItem = document.createElement('div');
        cartItem.className = 'cart-item';
        // PERUBAHAN: Tombol hapus sekarang menjadi ikon di sebelah kanan tombol +
        cartItem.innerHTML = `
            <img src="${item.img}" alt="${item.name}" class="cart-item-img">
            <div class="cart-item-details">
                <h4>${item.name}</h4>
                <p>Rp ${item.price.toLocaleString('id-ID')}</p>
            </div>
            <div class="cart-item-actions">
                <button onclick="updateQuantity(${item.id}, -1)">-</button>
                <span>${item.quantity}</span>
                <button onclick="updateQuantity(${item.id}, 1)">+</button>
                <button onclick="removeFromCart(${item.id})" class="cart-item-remove" title="Hapus Item">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M135.2 17.7L128 32H32C14.3 32 0 46.3 0 64S14.3 96 32 96H416c17.7 0 32-14.3 32-32s-14.3-32-32-32H320l-7.2-14.3C307.4 6.8 296.3 0 284.2 0H163.8c-12.1 0-23.2 6.8-28.6 17.7zM416 128H32L53.2 467c1.6 25.3 22.6 45 47.9 45H346.9c25.3 0 46.3-19.7 47.9-45L416 128z"/></svg>
                </button>
            </div>`;
        cartItemsContainer.appendChild(cartItem);
        total += item.price * item.quantity;
    });
    cartTotalElement.innerText = `Rp ${total.toLocaleString('id-ID')}`;
    setLanguage(localStorage.getItem('lang') || 'id'); // Update tombol hapus
}

function updateQuantity(productId, change) {
    let cart = JSON.parse(localStorage.getItem('cart')) || [];
    const item = cart.find(i => i.id === productId);
    if (item) { item.quantity += change; if (item.quantity <= 0) { cart = cart.filter(i => i.id !== productId); }}
    localStorage.setItem('cart', JSON.stringify(cart));
    loadCartItems();
    updateCartBadge();
}

function removeFromCart(productId) {
    let cart = JSON.parse(localStorage.getItem('cart')) || [];
    cart = cart.filter(item => item.id !== productId);
    localStorage.setItem('cart', JSON.stringify(cart));
    loadCartItems();
    updateCartBadge();
}

function checkoutWhatsApp() {
    const cart = JSON.parse(localStorage.getItem('cart')) || [];
    if (cart.length === 0) { alert("Keranjang Anda kosong."); return; }
    let message = "Halo Kak, saya mau pesan gelang dari Kairos Bracelet:\n\n";
    let total = 0;
    cart.forEach(item => { message += `*${item.name}*\nJumlah: ${item.quantity}\nHarga: Rp ${(item.price * item.quantity).toLocaleString('id-ID')}\n\n`; total += item.price * item.quantity; });
    message += `*Total Pesanan: Rp ${total.toLocaleString('id-ID')}*\n\nTerima kasih!`;
    const encodedMessage = encodeURIComponent(message);
    const whatsappURL = `https://wa.me/${noWhatsApp}?text=${encodedMessage}`;
    
    // Buka WhatsApp di tab baru
    window.open(whatsappURL, '_blank');

    // PERUBAHAN: Kosongkan keranjang setelah checkout
    localStorage.removeItem('cart'); // Hapus data dari storage
    loadCartItems();                 // Muat ulang tampilan keranjang (menjadi kosong)
    updateCartBadge();               // Perbarui notifikasi di header (menjadi 0)
}

function updateCartBadge() {
    const cart = JSON.parse(localStorage.getItem('cart')) || [];
    const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0); 
    const badge = document.querySelector('.cart-badge');
    if (badge) {
        if (totalItems > 0) { badge.textContent = totalItems; badge.style.display = 'inline-block'; } 
        else { badge.style.display = 'none'; }
    }
}

// ===================================================================================
// FUNGSI PILIHAN BAHASA
// ===================================================================================
const translations = {
    id: {
        productTitle: "Produk | Kairos Bracelet", cartTitle: "Keranjang Belanja | Kairos Bracelet", homeTitle: "Kairos Bracelet | Lucu & Unik", aboutTitle: "Tentang Kami | Kairos Bracelet", contactTitle: "Kontak | Kairos Bracelet",
        navHome: "Beranda", navProducts: "Produk", navCart: "Keranjang", navAbout: "Tentang Kami", navContact: "Kontak",
        heroTitle: "Gelang Lucu Buatan Tangan", heroSubtitle: "Koleksi terbaru dengan desain imut untuk ceriakan harimu!", heroButton: "Lihat Koleksi",
        bestsellerTitle: "Produk Terlaris Kami", buyNow: "Beli Sekarang", footerText: "© 2025 Kairos Bracelet | Dibuat Oleh Kel 12",
        allProducts: "Semua Produk Kami", addToCartBtn: "Masukkan ke Keranjang", cartHeader: "Keranjang Belanja Anda",
        emptyCart: "Keranjang belanja Anda masih kosong.", cartTotal: "Total:", checkoutButton: "Pesan via WhatsApp", removeBtn: "Hapus",
        aboutHeader: "Kisah di Balik Setiap Kilau Gelang",
        aboutText1: "Selamat datang di Kairos Bracelet! Kami percaya bahwa setiap perhiasan adalah cerita. Berawal dari hobi merangkai manik-manik, kami tumbuh menjadi sebuah brand yang didedikasikan untuk menciptakan kebahagiaan melalui gelang buatan tangan yang unik.",
        aboutText2: "Setiap gelang kami dirancang dengan detail, memadukan warna-warna pastel yang ceria dengan desain yang imut dan modern. Kami hanya menggunakan bahan-bahan berkualitas untuk memastikan setiap karya tidak hanya cantik, tetapi juga nyaman dan awet saat dipakai.",
        aboutText3: "Terima kasih telah menjadi bagian dari perjalanan kami. Mari ceriakan harimu dengan kilau dari koleksi kami!",
        contactHeader: "Hubungi Kami",
        contactText1: "Punya pertanyaan, kritik, atau saran? Kami senang mendengarnya! Jangan ragu untuk menghubungi kami melalui kanal di bawah ini.",
        contactText2: "Jam Operasional: Senin - Sabtu, 09:00 - 17:00 WIB.",
        modalUnitPrice: "Harga Satuan", modalTotalPrice: "Total Harga",
    },
    en: {
        productTitle: "Products | Kairos Bracelet", cartTitle: "Shopping Cart | Kairos Bracelet", homeTitle: "Kairos Bracelet | Cute & Unique", aboutTitle: "About Us | Kairos Bracelet", contactTitle: "Contact | Kairos Bracelet",
        navHome: "Home", navProducts: "Products", navCart: "Cart", navAbout: "About Us", navContact: "Contact",
        heroTitle: "Cute Handmade Bracelets", heroSubtitle: "Our newest collection with cute designs to brighten your day!", heroButton: "View Collection",
        bestsellerTitle: "Our Bestsellers", buyNow: "Buy Now", footerText: "© 2025 Kairos Bracelet | Created by Group 12",
        allProducts: "All Our Products", addToCartBtn: "Add to Cart", cartHeader: "Your Shopping Cart",
        emptyCart: "Your shopping cart is empty.", cartTotal: "Total:", checkoutButton: "Order via WhatsApp", removeBtn: "Remove",
        aboutHeader: "The Story Behind Every Sparkle",
        aboutText1: "Welcome to Kairos Bracelet! We believe that every piece of jewelry tells a story. Starting from a hobby of stringing beads, we have grown into a brand dedicated to creating happiness through unique handmade bracelets.",
        aboutText2: "Each of our bracelets is designed in detail, combining cheerful pastel colors with cute and modern designs. We only use high-quality materials to ensure that each work is not only beautiful, but also comfortable and durable.",
        aboutText3: "Thank you for being a part of our journey. Let's brighten your day with the sparkle from our collection!",
        contactHeader: "Contact Us",
        contactText1: "Have questions, feedback, or suggestions? We'd love to hear from you! Feel free to contact us through the channels below.",
        contactText2: "Operational Hours: Monday - Saturday, 09:00 - 17:00 WIB.",
        modalUnitPrice: "Unit Price", modalTotalPrice: "Total Price",
    }
};

function setLanguage(lang) {
    localStorage.setItem('lang', lang);
    document.querySelectorAll('[data-lang-key]').forEach(el => {
        const key = el.getAttribute('data-lang-key');
        const translation = translations[lang][key];
        if (translation !== undefined) {
            if (key === 'navCart') {
                const textNode = Array.from(el.childNodes).find(node => node.nodeType === Node.TEXT_NODE);
                if (textNode) textNode.textContent = translation;
            } else {
                el.textContent = translation;
            }
        }
    });
    
    if (document.getElementById('all-products-grid')) renderProducts();
    if (document.getElementById('cart-items-container')) loadCartItems();
    updateCartBadge();
}

document.addEventListener('DOMContentLoaded', () => {
    const savedLang = localStorage.getItem('lang') || 'id';
    setLanguage(savedLang);
});
