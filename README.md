import React, { useState } from "react";

// Fortune Rocks - Single-file React + Tailwind e-commerce template // Usage: drop into a Vite/CRA project with Tailwind configured. // - Replace product images with your own // - Connect to a backend or Shopify/WooCommerce when ready

export default function FortuneRocksApp() { const sampleProducts = [ { id: "lab-01", name: "Labradorite Palm Stone", price: 18, img: "https://images.unsplash.com/photo-1557180295-76eee20ae8aa?q=80&w=800&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder", intention: "Protection, Intuition", description: "A shimmering labradorite palm stone — protective and great for intuitive work.", }, { id: "am-01", name: "Chevron Amethyst Point", price: 24, img: "https://images.unsplash.com/photo-1543995535-7f3a2e1c7e2e?q=80&w=800&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder", intention: "Calm, Sleep Support", description: "Chevron amethyst point to soothe the mind and aid meditation.", }, { id: "cq-01", name: "Clear Quartz Cluster", price: 30, img: "https://images.unsplash.com/photo-1582719478179-2b6f4a0a9b3b?q=80&w=800&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder", intention: "Amplification, Clarity", description: "Clear quartz cluster to amplify intentions and energy work.", }, ];

const mysteryItems = [ { crystal: "Moonstone", fortune: "A new cycle begins — trust your intuition." }, { crystal: "Rose Quartz", fortune: "Open your heart; loving connections appear." }, { crystal: "Black Tourmaline", fortune: "Ground and release what no longer serves you." }, { crystal: "Citrine", fortune: "Prosperity energy is aligning in small, steady steps." }, ];

const [products] = useState(sampleProducts); const [cart, setCart] = useState([]); const [showCart, setShowCart] = useState(false); const [checkoutMessage, setCheckoutMessage] = useState(null);

function addToCart(product) { setCart((c) => { const found = c.find((x) => x.id === product.id); if (found) return c.map((x) => (x.id === product.id ? { ...x, qty: x.qty + 1 } : x)); return [...c, { ...product, qty: 1 }]; }); }

function removeFromCart(id) { setCart((c) => c.filter((x) => x.id !== id)); }

function changeQty(id, qty) { if (qty < 1) return; setCart((c) => c.map((x) => (x.id === id ? { ...x, qty } : x))); }

function pickMystery() { const r = mysteryItems[Math.floor(Math.random() * mysteryItems.length)]; return r; }

function checkout() { // This is a stub for demo — integrate with real checkout provider for production const mystery = pickMystery(); const subtotal = cart.reduce((s, p) => s + p.price * p.qty, 0); setCheckoutMessage({ subtotal, mystery }); setCart([]); setShowCart(false); }

return ( <div className="min-h-screen bg-gradient-to-b from-purple-50 via-white to-pink-50 text-gray-800"> {/* Header */} <header className="max-w-6xl mx-auto p-4 flex items-center justify-between"> <div className="flex items-center gap-4"> <div className="w-12 h-12 bg-gradient-to-br from-purple-300 to-pink-300 rounded-full flex items-center justify-center shadow-md"> <span className="font-bold text-white">FR</span> </div> <div> <h1 className="text-2xl font-extrabold">Fortune Rocks</h1> <p className="text-sm text-gray-600">Crystals chosen to align your energy</p> </div> </div>

<nav className="flex items-center gap-4">
      <button
        className="px-3 py-2 rounded-md hover:bg-gray-100"
        onClick={() => window.scrollTo({ top: 0, behavior: "smooth" })}
      >
        Home
      </button>
      <button
        className="px-3 py-2 rounded-md hover:bg-gray-100"
        onClick={() => document.getElementById("shop-section").scrollIntoView({ behavior: "smooth" })}
      >
        Shop
      </button>
      <button
        className="px-3 py-2 rounded-md hover:bg-gray-100"
        onClick={() => document.getElementById("about-section").scrollIntoView({ behavior: "smooth" })}
      >
        About
      </button>
      <button
        className="px-3 py-2 rounded-md bg-purple-600 text-white rounded shadow"
        onClick={() => setShowCart(true)}
      >
        Cart ({cart.reduce((s, p) => s + p.qty, 0)})
      </button>
    </nav>
  </header>

  {/* Hero */}
  <section className="max-w-6xl mx-auto p-6 grid md:grid-cols-2 gap-8 items-center">
    <div>
      <h2 className="text-4xl font-extrabold leading-tight">Find the crystal that calls to you ✨</h2>
      <p className="mt-4 text-gray-600">
        Every purchase includes a mystery crystal gift and a playful, intuitive fortune written by me — a certified
        crystal & energy healer.
      </p>

      <div className="mt-6 flex gap-3">
        <button
          className="px-5 py-3 bg-purple-600 text-white rounded shadow hover:opacity-95"
          onClick={() => document.getElementById("shop-section").scrollIntoView({ behavior: "smooth" })}
        >
          Shop Crystals
        </button>
        <a
          className="px-5 py-3 border rounded text-purple-700 hover:bg-purple-50"
          href="#about-section"
        >
          Learn About Me
        </a>
      </div>

      <div className="mt-8 p-4 bg-white rounded-lg shadow-sm">
        <h3 className="font-semibold">How it works</h3>
        <ol className="mt-2 text-sm text-gray-600 space-y-1">
          <li>1. Choose a crystal from the shop</li>
          <li>2. With every purchase you receive a mystery crystal + an intuitive fortune</li>
          <li>3. Use the crystals with the intention listed to balance energy</li>
        </ol>
      </div>
    </div>

    <div className="rounded-lg overflow-hidden shadow-lg">
      <img
        src="https://images.unsplash.com/photo-1519681393784-d120267933ba?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder"
        alt="crystals hero"
        className="w-full h-80 object-cover"
      />
    </div>
  </section>

  {/* Shop */}
  <section id="shop-section" className="max-w-6xl mx-auto p-6">
    <h3 className="text-2xl font-bold mb-4">Shop Crystals</h3>
    <div className="grid md:grid-cols-3 gap-6">
      {products.map((p) => (
        <div key={p.id} className="bg-white rounded-lg shadow p-4 flex flex-col">
          <img src={p.img} alt={p.name} className="h-44 w-full object-cover rounded" />
          <div className="mt-3 flex-1">
            <h4 className="font-semibold">{p.name}</h4>
            <p className="text-sm text-gray-500">{p.intention}</p>
            <p className="mt-2 text-sm text-gray-700">{p.description}</p>
          </div>
          <div className="mt-4 flex items-center justify-between">
            <div>
              <span className="text-lg font-bold">${p.price}</span>
            </div>
            <div className="flex gap-2">
              <button
                onClick={() => addToCart(p)}
                className="px-3 py-2 bg-purple-600 text-white rounded shadow-sm"
              >
                Add to cart
              </button>
            </div>
          </div>
        </div>
      ))}
    </div>
  </section>

  {/* Mystery Gift Callout */}
  <section className="max-w-6xl mx-auto p-6">
    <div className="bg-gradient-to-r from-purple-100 to-pink-50 rounded-lg p-6 flex items-center gap-6">
      <div className="w-24 h-24 bg-white rounded-full flex items-center justify-center shadow">🔮</div>
      <div>
        <h4 className="text-xl font-semibold">Mystery Crystal Gift</h4>
        <p className="text-gray-600 mt-1">Every order includes a surprise crystal & a short intuitive fortune — free!</p>
        <p className="text-sm text-gray-500 mt-2">Want more mystery gifts? Add extras at checkout.</p>
      </div>
    </div>
  </section>

  {/* About */}
  <section id="about-section" className="max-w-6xl mx-auto p-6 bg-white rounded-lg shadow mt-4">
    <div className="md:flex gap-6 items-center">
      <img
        src="https://images.unsplash.com/photo-1542444459-db1d3b4c8b3b?q=80&w=600&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder"
        alt="owner"
        className="w-48 h-48 object-cover rounded-lg shadow"
      />
      <div>
        <h3 className="text-2xl font-bold">About the healer</h3>
        <p className="mt-2 text-gray-700">
          Hi — I'm a certified crystal & energy healer and intuitive. I hand-select each crystal with care, and write
          a short, intuitive fortune to accompany every order. My goal is to share compassion and help you align
          your energy — whether you're new to crystals or a longtime collector.
        </p>
        <ul className="mt-3 text-sm text-gray-600 space-y-1">
          <li>• Certified crystal healer</li>
          <li>• Intuitive readings included with every order</li>
          <li>• Ethically sourced crystals</li>
        </ul>
      </div>
    </div>
  </section>

  {/* Contact / Footer */}
  <footer className="max-w-6xl mx-auto p-6 mt-8 text-sm text-gray-600">
    <div className="md:flex justify-between items-start">
      <div>
        <h4 className="font-semibold">Fortune Rocks</h4>
        <p className="mt-2">Subscribe for restocks and mini-readings.</p>
        <form className="mt-3 flex gap-2">
          <input
            type="email"
            placeholder="you@example.com"
            className="px-3 py-2 border rounded w-64"
          />
          <button className="px-3 py-2 bg-purple-600 text-white rounded">Subscribe</button>
        </form>
      </div>

      <div className="mt-6 md:mt-0">
        <h5 className="font-semibold">Contact</h5>
        <p className="mt-2">hello@fortunerocks.example</p>
        <p className="mt-1">FAQ | Shipping | Returns</p>
      </div>
    </div>

    <div className="mt-6 text-gray-500">© {new Date().getFullYear()} Fortune Rocks</div>
  </footer>

  {/* Cart Drawer */}
  {showCart && (
    <div className="fixed inset-0 bg-black/40 z-40 flex justify-end">
      <div className="w-full md:w-96 bg-white p-6 shadow-lg">
        <div className="flex items-center justify-between">
          <h4 className="font-bold">Your cart</h4>
          <button onClick={() => setShowCart(false)}>Close</button>
        </div>

        <div className="mt-4 space-y-4">
          {cart.length === 0 && <p className="text-sm text-gray-500">Your cart is empty.</p>}
          {cart.map((item) => (
            <div key={item.id} className="flex items-center gap-3">
              <img src={item.img} alt={item.name} className="w-16 h-16 object-cover rounded" />
              <div className="flex-1">
                <div className="flex justify-between">
                  <div>
                    <div className="font-semibold">{item.name}</div>
                    <div className="text-sm text-gray-500">{item.intention}</div>
                  </div>
                  <div>${item.price * item.qty}</div>
                </div>
                <div className="mt-2 flex items-center gap-2">
                  <button onClick={() => changeQty(item.id, item.qty - 1)} className="px-2">-</button>
                  <div className="px-2">{item.qty}</div>
                  <button onClick={() => changeQty(item.id, item.qty + 1)} className="px-2">+</button>
                  <button onClick={() => removeFromCart(item.id)} className="ml-4 text-sm text-red-500">Remove</button>
                </div>
              </div>
            </div>
          ))}
        </div>

        <div className="mt-6">
          <div className="flex justify-between text-gray-700">
            <div className="font-semibold">Subtotal</div>
            <div className="font-semibold">${cart.reduce((s, p) => s + p.price * p.qty, 0)}</div>
          </div>
          <div className="mt-4">
            <button
              onClick={checkout}
              className="w-full px-4 py-3 bg-purple-600 text-white rounded font-semibold"
              disabled={cart.length === 0}
            >
              Checkout
            </button>
          </div>
        </div>
      </div>
    </div>
  )}

  {/* Checkout message modal */}
  {checkoutMessage && (
    <div className="fixed inset-0 z-50 flex items-center justify-center">
      <div className="bg-black/40 absolute inset-0" onClick={() => setCheckoutMessage(null)}></div>
      <div className="bg-white rounded-lg p-6 z-50 max-w-md mx-4 shadow-lg">
        <h4 className="font-bold">Thank you for your order!</h4>
        <p className="mt-2 text-gray-600">Subtotal: ${checkoutMessage.subtotal}</p>
        <div className="mt-4 p-4 bg-purple-50 rounded">
          <p className="text-sm">Your free mystery crystal: <span className="font-semibold">{checkoutMessage.mystery.crystal}</span></p>
          <p className="mt-2 italic">"{checkoutMessage.mystery.fortune}"</p>
        </div>
        <div className="mt-4 text-right">
          <button onClick={() => setCheckoutMessage(null)} className="px-4 py-2 bg-purple-600 text-white rounded">Close</button>
        </div>
      </div>
    </div>
  )}
</div>

); }

