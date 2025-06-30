<template>
    <div class="payment-summary">
        <h2>Payment Summary</h2>

        <!-- Pizza Tyoe -->
        <div class="summary-item">
            <span>{{ pizza?.name || 'None' }}</span>
            <span v-if="basePrice">{{ basePrice.toFixed(1) }}$</span>
        </div>

        <!-- Pizza Size -->
        <div class="summary-item">
            <span v-if="size">Size - {{ size.name }}</span>
            <span v-if="size?.extra_price > -1">{{ size.extra_price }}$</span>
            <span v-else class="default" style="opacity: 0.5;">Size</span>
        </div>

        <!-- Pizza Toppings -->
        <div v-for="topping in toppings" :key="topping.id" class="summary-item">
            <span>{{ topping.name }}</span>
            <span>{{ topping.price }}$</span>
        </div>

        <!-- Total Price -->
        <div class="total-price">
            <span class="label">Total Price</span>
            <span class="price">${{ totalPrice.toFixed(2) }}</span>
        </div>

        <button class="order-button" @click="orderNow" :disabled="!pizza || !size">
            Order Now
        </button>
    </div>

    <!-- Success Modal -->
    <div class="modal-backdrop" v-if="showModal">
        <div class="modal-card">
            <h3>🎉 Order Success!</h3>
            <p>Thank you. We have received your order successfully. </p>
            <button class="close-button" @click="closeModal">Close</button>
        </div>
    </div>
</template>


<script>
export default {
    name: "OrderSummary",
    props: {
        pizza: Object,
        size: Object,
        toppings: Array,
    },
    computed: {
        basePrice() {
            return this.pizza?.discount?.is_active
                ? this.pizza.discount.final_price
                : this.pizza?.price || 0;
        },
        totalPrice() {
            const sizePrice = this.size?.extra_price || 0;
            const toppingTotal = this.toppings.reduce((sum, t) => sum + t.price, 0);
            return this.basePrice + sizePrice + toppingTotal;
        }
    },
    data() {
        return {
            showModal: false
        };
    },
    methods: {
        orderNow() {
            this.showModal = true;
        },
        closeModal() {
            this.showModal = false;
            this.$emit('reset');
        }
    }
};
</script>

<style scoped>
.payment-summary {
    background-color: #FFFFFF;
    border-radius: 12px;
    padding: 20px;
    color: #333333;
    box-shadow: 0 7px 15px rgba(0, 0, 0, 0.1);
    ;
}

.payment-summary h2 {
    font-size: medium;
    color: #E77E23;
    margin-bottom: 10px;
}

.summary-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 14px;
    padding: 5px 10px;
    color: #6C7881;
}

.summary-item:last-of-type {
    border-bottom: 1px solid;
}

.total-price {
    font-size: medium;
    margin-top: 1.5rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.total-price .label {
    color: #333333;
}

.total-price .price {
    color: #f57c00;
    font-weight: bold;
}

.order-button {
    background-color: #f57c00;
    color: white;
    padding: 10px 10px;
    border: none;
    border-radius: 50px;
    font-weight: bold;
    cursor: pointer;
    margin-top: 20px;
    width: 100%;
}

.order-button:hover {
    background-color: #e96b00;
}

.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-card {
  background: white;
  padding: 30px;
  border-radius: 5px;
  text-align: center;
  max-width: 300px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.3);
}

.modal-card h3 {
  color: #333333;
  margin-bottom: 10px;
}

.modal-card p {
    font-size: small;
    color: #333333;
}

.close-button {
  margin-top: 30px;
  font-weight: bold;
  width: 90%;
  background-color: #e96b00;
  color: white;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 50px;
  cursor: pointer;
}

.close-button:hover {
  background-color: #e96b00;
}
</style>