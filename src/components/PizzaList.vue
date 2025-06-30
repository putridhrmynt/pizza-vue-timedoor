<template>
    <section>
        <h2 class="menu-title">Choose your pizza</h2>
        <!-- Pizza Type  -->
        <div class="pizza-grid">
            <label v-for="pizza in pizzas" :key="pizza.id" class="pizza-label">
                <input type="radio" :value="pizza.id" v-model="selectedPizzaId" class="hidden-radio"
                    @change="$emit('select', pizza)" />
                <div class="pizza-card" :class="{ selected: selectedPizzaId === pizza.id }">
                    <img v-if="pizza.discount.is_active" :src="ribbonImage" alt="Discount" class="ribbon" />
                    <img :src="getPizzaImage(pizza.id)" class="pizza-image" :alt="pizza.name" />
                    <div class="pizza-info">
                        <h3>{{ pizza.name }}</h3>
                        <p class="price">
                            <span v-if="pizza.discount.is_active">
                                <span>${{ pizza.discount.final_price }}</span> <s>${{ pizza.price }}</s>
                            </span>
                            <span v-else>
                                ${{ pizza.price }}
                            </span>
                        </p>
                    </div>
                </div>
            </label>

        </div>
    </section>
</template>


<script>
import pizzaData from '@/assets/pizza-list.json';
import ribbon from '@/assets/ribbon.svg';

export default {
    name: "PizzaList",
    data() {
        return {
            pizzas: pizzaData.data,
            ribbonImage: ribbon,
            selectedPizzaId: null,
        };
    },
    methods: {
        getPizzaImage(id) {
            return new URL(`../assets/pizza${id}.png`, import.meta.url).href;
        }
    }
};
</script>

<style scoped>
.hidden-radio {
    display: none;
}

.menu-title {
    font-size: 2rem;
    color: #E77E23;
    margin-bottom: 2rem;
}

.pizza-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
    gap: 20px;
}

.pizza-card {
    display: flex;
    position: relative;
    background-color: #F8F8F6;
    border-radius: 12px;
    border: solid rgb(231, 231, 231) 0.1px;
    overflow: hidden;
    transition: transform 0.2s;
    align-items: center;
    padding: 1rem;
    gap: 1rem;
    cursor: pointer;
}

.pizza-card:hover {
    background-color: #F8D8BD;
    transition: background-color 0.5s ease;
}

.pizza-card.selected {
    background-color: #E77E23;
}

.ribbon {
    position: absolute;
    top: 0;
    right: 0;
    width: 90px;
    height: auto;
    z-index: 2;
}

.pizza-image {
    width: 100px;
    height: 100px;
    object-fit: contain;
    margin: 8px;
}

.pizza-card:hover .pizza-image {
    transform: rotate(15deg);
    transition: 0.5s ease;
}

.pizza-card.selected .pizza-image {
    transform: rotate(15deg);
}

.pizza-card.selected .pizza-info,
.pizza-card.selected .pizza-info .price s {
    color: #F8F8F6;
}

.pizza-info {
    text-align: left;
    font-size: 12px;
    color: #333333;
}

.price {
    margin-top: 3px;
}

.price s {
    color: gray;
    margin-right: 0.5rem;
    font-weight: normal;
}
</style>