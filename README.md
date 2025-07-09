# Cosmo-cuiimport React, { useState } from "react"; import { Button } from "@/components/ui/button"; import { Card, CardContent } from "@/components/ui/card"; import { Phone, MapPin, Instagram } from "lucide-react"; import { initializeApp } from "firebase/app"; import { getFirestore, collection, addDoc } from "firebase/firestore";

// Firebase config (Replace with your actual config) const firebaseConfig = { apiKey: "YOUR_API_KEY", authDomain: "YOUR_AUTH_DOMAIN", projectId: "YOUR_PROJECT_ID", storageBucket: "YOUR_STORAGE_BUCKET", messagingSenderId: "YOUR_SENDER_ID", appId: "YOUR_APP_ID" };

const app = initializeApp(firebaseConfig); const db = getFirestore(app);

export default function HomePage() { const [form, setForm] = useState({ name: "", phone: "", dish: "" }); const [success, setSuccess] = useState(false);

const handleSubmit = async (e) => { e.preventDefault(); try { await addDoc(collection(db, "orders"), form); setSuccess(true); setForm({ name: "", phone: "", dish: "" }); } catch (err) { console.error("Error submitting order:", err); } };

return ( <div className="min-h-screen bg-white text-gray-800"> {/* Hero Section */} <section className="bg-[url('/hero.jpg')] bg-cover bg-center text-white h-[90vh] flex items-center justify-center"> <div className="bg-black/50 p-10 rounded-xl text-center"> <h1 className="text-4xl md:text-6xl font-bold mb-4">Cosmo Cuisine</h1> <p className="text-lg md:text-2xl mb-6">A Taste of Flavorful Elegance</p> <Button className="bg-yellow-500 text-black hover:bg-yellow-600">Order Now</Button> </div> </section>

{/* Menu Preview */}
  <section className="py-16 px-4 md:px-20">
    <h2 className="text-3xl font-bold text-center mb-10">Our Signature Dishes</h2>
    <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
      {["Grilled Chicken", "Jollof Rice", "Plantain Fries"].map((dish, i) => (
        <Card key={i} className="rounded-2xl shadow-md">
          <CardContent className="p-4">
            <img src={`/dish${i + 1}.jpg`} alt={dish} className="rounded-xl mb-4" />
            <h3 className="text-xl font-semibold">{dish}</h3>
            <p className="text-sm text-gray-600">Delicious and satisfying, made fresh to order.</p>
          </CardContent>
        </Card>
      ))}
    </div>
  </section>

  {/* Order Section */}
  <section className="py-16 px-4 md:px-20 bg-yellow-50">
    <div className="max-w-2xl mx-auto">
      <h2 className="text-3xl font-bold text-center mb-8">Place an Order</h2>
      <form onSubmit={handleSubmit} className="space-y-6">
        <div>
          <label className="block mb-1 font-medium">Name</label>
          <input
            type="text"
            className="w-full p-3 border rounded-lg"
            value={form.name}
            onChange={(e) => setForm({ ...form, name: e.target.value })}
            required
          />
        </div>
        <div>
          <label className="block mb-1 font-medium">Phone</label>
          <input
            type="text"
            className="w-full p-3 border rounded-lg"
            value={form.phone}
            onChange={(e) => setForm({ ...form, phone: e.target.value })}
            required
          />
        </div>
        <div>
          <label className="block mb-1 font-medium">Dish</label>
          <select
            className="w-full p-3 border rounded-lg"
            value={form.dish}
            onChange={(e) => setForm({ ...form, dish: e.target.value })}
            required
          >
            <option value="">Select a dish</option>
            <option value="Grilled Chicken">Grilled Chicken</option>
            <option value="Jollof Rice">Jollof Rice</option>
            <option value="Plantain Fries">Plantain Fries</option>
          </select>
        </div>
        <Button type="submit" className="w-full bg-yellow-500 text-black hover:bg-yellow-600">Submit Order</Button>
        {success && <p className="text-green-600 text-center">Your order has been placed!</p>}
      </form>
    </div>
  </section>

  {/* About Section */}
  <section className="bg-gray-100 py-16 px-4 md:px-20">
    <div className="max-w-4xl mx-auto text-center">
      <h2 className="text-3xl font-bold mb-6">Our Story</h2>
      <p className="text-lg text-gray-700">Cosmo Cuisine was born from the love of African flavor and modern experience. Our mission is to serve unforgettable meals with a touch of home and a pinch of innovation.</p>
    </div>
  </section>

  {/* Contact & Footer */}
  <footer className="bg-black text-white py-10 px-4 md:px-20">
    <div className="grid grid-cols-1 md:grid-cols-3 gap-6 text-center md:text-left">
      <div>
        <h4 className="text-lg font-semibold mb-2">Location</h4>
        <p className="flex items-center justify-center md:justify-start gap-2"><MapPin size={18} /> Kentinkrono, Kumasi</p>
      </div>
      <div>
        <h4 className="text-lg font-semibold mb-2">Contact</h4>
        <p className="flex items-center justify-center md:justify-start gap-2"><Phone size={18} /> 0536805617</p>
      </div>
      <div>
        <h4 className="text-lg font-semibold mb-2">Follow Us</h4>
        <p className="flex items-center justify-center md:justify-start gap-2"><Instagram size={18} /> @cosmocuisine</p>
      </div>
    </div>
    <div className="text-center mt-10 text-sm text-gray-400">&copy; {new Date().getFullYear()} Cosmo Cuisine. All rights reserved.</div>
  </footer>
</div>

); }



