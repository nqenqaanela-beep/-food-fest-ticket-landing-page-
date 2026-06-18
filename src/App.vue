<script setup>
import { ref } from 'vue'
import TicketCard from './components/TicketCard.vue'

// Localized Event Data Object Array matching project brief specifications
const ticketTiers = ref([
  {
    id: 1,
    name: 'Bronze Tier',
    price: 150,
    description: 'Perfect for casual foodies looking to explore the festival grounds and grab a bite.',
    isFeatured: false,
    benefits: [
      'General Admission access for 1 Day',
      'Complimentary branded tasting glass',
      'Access to standard food trucks & live music stages',
      'Free parking voucher'
    ]
  },
  {
    id: 2,
    name: 'Silver Tier',
    price: 380,
    description: 'The definitive festival experience. Includes exclusive tasting tokens and masterclass seatings.',
    isFeatured: true, // Used to satisfy requirement 2: Highlight featured tier
    benefits: [
      'Full Weekend Access Pass',
      '50 Curated Food & Beverage Tasting Tokens',
      'Priority seating at chef demonstration masterclasses',
      'Access to shaded seating lounges'
    ]
  },
  {
    id: 3,
    name: 'Gold Tier',
    price: 850,
    description: 'The ultimate VIP culinary indulgence. Premium drinks, private viewing decks, and artisan gift bags.',
    isFeatured: false,
    benefits: [
      'VIP Fast-Track festival entrance lanes',
      'Unlimited access to the Private VIP Cocktail Lounge',
      'Complimentary multi-course tasting menu curated by top chefs',
      'Premium artisan take-home gift box'
    ]
  }
])

// State manager for tracking favorites (Requirement 3)
const favoritedTickets = ref([])

// Toggle interaction handler
const handleToggleFavorite = (ticketName) => {
  if (favoritedTickets.value.includes(ticketName)) {
    favoritedTickets.value = favoritedTickets.value.filter(item => item !== ticketName)
  } else {
    favoritedTickets.value.push(ticketName)
  }
}
</script>

<template>
  <div class="festival-container">
    <header class="fest-header">
      <div class="header-top">
        <h1 class="brand-logo">CPT Food<span>Fest</span></h1>
        <div class="wishlist-counter" :class="{ 'has-items': favoritedTickets.length > 0 }">
          <span class="heart-icon">❤️</span> Saved Tiers: <strong>{{ favoritedTickets.length }}</strong>
        </div>
      </div>
      
      <div class="hero-content">
        <h2>Taste the Flavours of Cape Town</h2>
        <p>Join us for an unforgettable weekend of elite culinary creations, local artisan food trucks, and live music beneath Table Mountain. Explore our flexible pricing tiers and lock down your spot today.</p>
      </div>
    </header>

    <div v-if="favoritedTickets.length > 0" class="saved-summary-alert">
      🎉 You are actively comparing these experiences: <strong>{{ favoritedTickets.join(', ') }}</strong>!
    </div>

    <main class="tickets-grid">
      <TicketCard 
        v-for="ticket in ticketTiers" 
        :key="ticket.id"
        :ticketData="ticket"
        :isSaved="favoritedTickets.includes(ticket.name)"
        @toggle-saved="handleToggleFavorite"
      />
    </main>

    <footer class="fest-footer">
      <div class="cta-box">
        <h3>Don't Miss the Biggest Culinary Weekend of 2026</h3>
        <p>Subscribe to secure absolute priority access when the transactional ticketing engine officially goes live.</p>
        <div class="newsletter-input-group">
          <input type="email" placeholder="Enter your email address" @keyup.enter="alert('Thank you! We will notify you instantly.')">
          <button @click="alert('Thank you! We will notify you instantly.')">Notify Me</button>
        </div>
      </div>
      <p class="copyright">&copy; 2026 Cape Town Food Fest. Engineering Framework Built Proudly with Vue.js 3.</p>
    </footer>
  </div>
</template>

<style>
/* Base Professional Typography & Theming Map Variables */
:root {
  --primary-orange: #f97316;
  --secondary-dark: #0f172a;
  --bg-canvas: #f8fafc;
  --text-muted: #64748b;
  --shadow-sm: 0 4px 6px -1px rgb(0 0 0 / 0.05);
}

body {
  margin: 0;
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
  background-color: var(--bg-canvas);
  color: #1e293b;
}

.festival-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.fest-header {
  margin-bottom: 40px;
  background: white;
  padding: 30px;
  border-radius: 16px;
  box-shadow: var(--shadow-sm);
}

.header-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #e2e8f0;
  padding-bottom: 20px;
  margin-bottom: 30px;
}

.brand-logo {
  font-size: 1.8rem;
  font-weight: 800;
  color: var(--secondary-dark);
  margin: 0;
}

.brand-logo span {
  color: var(--primary-orange);
}

.wishlist-counter {
  background: #f1f5f9;
  padding: 10px 18px;
  border-radius: 30px;
  font-size: 0.95rem;
  color: #475569;
  transition: all 0.3s ease;
}

.wishlist-counter.has-items {
  background: #ffedd5;
  color: #ea580c;
  transform: scale(1.05);
}

.hero-content h2 {
  font-size: 2.4rem;
  color: var(--secondary-dark);
  margin-bottom: 12px;
  letter-spacing: -0.5px;
}

.hero-content p {
  color: var(--text-muted);
  font-size: 1.1rem;
  line-height: 1.6;
  margin: 0;
}

.saved-summary-alert {
  background-color: #f0fdf4;
  border: 1px solid #bbf7d0;
  color: #166534;
  padding: 14px 20px;
  border-radius: 8px;
  margin-bottom: 30px;
  font-size: 0.95rem;
  text-align: center;
}

/* Flexible Grid System Layout Rule */
.tickets-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 30px;
  margin-bottom: 50px;
}

.cta-box {
  background: var(--secondary-dark);
  color: white;
  padding: 40px;
  border-radius: 16px;
  text-align: center;
  margin-bottom: 30px;
}

.cta-box h3 {
  font-size: 1.6rem;
  margin-bottom: 10px;
}

.cta-box p {
  color: #94a3b8;
  margin-bottom: 25px;
}

.newsletter-input-group {
  display: flex;
  max-width: 500px;
  margin: 0 auto;
  gap: 10px;
}

.newsletter-input-group input {
  flex: 1;
  padding: 14px 20px;
  border-radius: 8px;
  border: none;
  outline: none;
  font-size: 1rem;
}

.newsletter-input-group button {
  background: var(--primary-orange);
  color: white;
  border: none;
  padding: 14px 28px;
  font-weight: 600;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s;
}

.newsletter-input-group button:hover {
  background: #ea580c;
}

.copyright {
  text-align: center;
  font-size: 0.85rem;
  color: var(--text-muted);
}

/* Mobile Breakpoint Responsiveness (Requirement 6) */
@media (max-width: 640px) {
  .header-top {
    flex-direction: column;
    gap: 15px;
    align-items: flex-start;
  }
  .hero-content h2 {
    font-size: 1.8rem;
  }
  .newsletter-input-group {
    flex-direction: column;
  }
}
</style>
