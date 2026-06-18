<script setup>
// Explicit Prop mappings feeding content from parent data layer
defineProps({
  ticketData: {
    type: Object,
    required: true
  },
  isSaved: {
    type: Boolean,
    default: false
  }
})

// Declared internal emit pipelines routing interactions back out
defineEmits(['toggle-saved'])
</script>

<template>
  <div class="ticket-card" :class="{ 'featured-highlight-style': ticketData.isFeatured }">
    
    <div v-if="ticketData.isFeatured" class="featured-badge">
      🔥 MOST POPULAR EXP
    </div>

    <div class="card-body">
      <div class="card-header-row">
        <h3 class="tier-name">{{ ticketData.name }}</h3>
        <button 
          @click="$emit('toggle-saved', ticketData.name)" 
          class="fav-toggle-btn"
          :class="{ 'is-active-heart': isSaved }"
        >
          {{ isSaved ? '❤️' : '🤍' }}
        </button>
      </div>

      <div class="price-container">
        <span class="currency">R</span>
        <span class="amount">{{ ticketData.price }}</span>
        <span class="period">/ ticket</span>
      </div>

      <p class="tier-description">{{ ticketData.description }}</p>

      <ul class="benefit-list">
        <li v-for="(benefit, index) in ticketData.benefits" :key="index">
          <span class="check-mark">✔</span> {{ benefit }}
        </li>
      </ul>
    </div>

    <div class="card-action-footer">
      <button class="purchase-cta-btn" @click="alert(`Redirecting to lock down your ${ticketData.name}!`)">
        Select Experience
      </button>
    </div>
  </div>
</template>

<style scoped>
/* Component Isolated CSS Rulesets preventing layout leakage cascading patterns */
.ticket-card {
  background: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 14px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  position: relative;
  transition: all 0.3s ease;
}

.ticket-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 20px -8px rgb(0 0 0 / 0.08);
}

/* Distinctive styling highlight configurations for Featured cards */
.ticket-card.featured-highlight-style {
  border: 2px solid #f97316;
  box-shadow: 0 10px 25px -5px rgba(249, 115, 22, 0.15);
}

.featured-badge {
  position: absolute;
  top: -12px;
  left: 50%;
  transform: translateX(-50%);
  background: linear-gradient(135deg, #f97316, #ea580c);
  color: white;
  font-size: 0.75rem;
  font-weight: 700;
  padding: 6px 14px;
  border-radius: 20px;
  white-space: nowrap;
}

.card-body {
  padding: 30px;
}

.card-header-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
}

.tier-name {
  font-size: 1.4rem;
  font-weight: 700;
  color: #0f172a;
  margin: 0;
}

.fav-toggle-btn {
  background: none;
  border: none;
  font-size: 1.4rem;
  cursor: pointer;
  transition: transform 0.2s;
}

.fav-toggle-btn:hover {
  transform: scale(1.2);
}

.price-container {
  display: flex;
  align-items: baseline;
  margin-bottom: 20px;
}

.currency {
  font-size: 1.2rem;
  font-weight: 600;
  margin-right: 2px;
}

.amount {
  font-size: 2.4rem;
  font-weight: 800;
  line-height: 1;
}

.period {
  font-size: 0.85rem;
  color: #64748b;
  margin-left: 6px;
}

.tier-description {
  color: #475569;
  font-size: 0.95rem;
  line-height: 1.5;
  margin-bottom: 25px;
}

.benefit-list {
  list-style: none;
  padding: 0;
  margin: 0;
  border-top: 1px solid #f1f5f9;
  padding-top: 20px;
}

.benefit-list li {
  font-size: 0.95rem;
  color: #334155;
  margin-bottom: 12px;
  display: flex;
  align-items: flex-start;
}

.check-mark {
  color: #10b981;
  font-weight: bold;
  margin-right: 10px;
}

.card-action-footer {
  padding: 0 30px 35px 30px;
}

.purchase-cta-btn {
  width: 100%;
  background-color: #0f172a;
  color: white;
  border: none;
  padding: 14px;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s;
}

.purchase-cta-btn:hover {
  background-color: #1e293b;
}

.featured-highlight-style .purchase-cta-btn {
  background-color: #f97316;
}

.featured-highlight-style .purchase-cta-btn:hover {
  background-color: #ea580c;
}
</style>