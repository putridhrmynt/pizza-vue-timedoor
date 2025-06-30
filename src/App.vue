<template>
  <div id="app">
    <HeroSection />
    <div class="gray-background">
      <div class="main-content">
        <div class="left-column">
          <PizzaList @select="handleSelectPizza" />
          <CustomPizza :pizza="selectedPizza || defaultPizza" @customize="handleCustomize" />
        </div>
        <div class="right-column">
          <OrderSummary :pizza="selectedPizza || defaultPizza" :size="selectedSize" :toppings="selectedToppings"
            @reset="resetSelections" />
        </div>
      </div>
      <FooterSection />
    </div>
  </div>
</template>

<script>
import HeroSection from './components/HeroSection.vue';
import PizzaList from './components/PizzaList.vue';
import CustomPizza from './components/CustomPizza.vue';
import toppingData from '@/assets/topping-list.json';
import OrderSummary from './components/OrderSummary.vue';
import FooterSection from './components/FooterSection.vue';

export default {
  name: 'App',
  components: {
    HeroSection,
    PizzaList,
    CustomPizza,
    OrderSummary,
    FooterSection,
  },
  data() {
    return {
      selectedPizza: null,
      selectedSize: null,
      selectedToppings: [],
      customizedPizza: null,
      defaultPizza: {
        id: 0,
        name: 'Custom Pizza',
        price: 0,
        discount: {
          is_active: false,
          final_price: 0
        },
        toppings: toppingData.data.map(t => t.id)
      }
    };
  },
  methods: {
    handleSelectPizza(pizza) {
      this.selectedPizza = pizza;
    },
    handleCustomize(data) {
      this.selectedPizza = data.pizza;
      this.selectedSize = data.size;
      this.selectedToppings = data.toppings;
    },
    resetSelections() {
      this.selectedPizza = null;
      this.selectedSize = null;
      this.selectedToppings = [];
    }
  }
};
</script>

<style>
.gray-background {
  background-color: #F8F8F6;
  padding-top: 110px;
  padding-inline: 90px;
  padding-bottom: 20px;
}

.main-content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 2rem;
}

.left-column {
  flex: 3.5;
}

.right-column {
  flex: 1.1;
  top: 90px;
}
</style>
