<template>
    <section class="custom-pizza">
        <h2>Custom Pizza</h2>

        <!-- Size Selection -->
        <div class="custom-section">
            <h3>Size</h3>
            <div class="size-option">
                <label v-for="size in sizes" :key="size.id" class="radio-label">
                    <input type="radio" :value="size" v-model="selectedSize" name="size" class="styled-radio"
                        @change="emitCustomization" />
                    {{ size.name }}
                    <span v-if="size.extra_price > 0" class="extra-price">
                        (+${{ size.extra_price }})
                    </span>
                </label>
            </div>
        </div>

        <!-- Topping Selection -->
        <div class="custom-section">
            <h3>Toppings</h3>
            <div class="topping-grid">
                <label v-for="topping in toppings" :key="topping.id" class="topping-pill"
                    :class="{ selected: selectedToppingIds.includes(topping.id), disabled: !isAvailable(topping.id) }">
                    <input type="checkbox" :value="topping.id" v-model="selectedToppingIds"
                        :disabled="!isAvailable(topping.id)" class="hidden-checkbox" @change="emitCustomization" />
                    {{ topping.name }}
                </label>
            </div>
        </div>

    </section>
</template>

<script>
import sizes from '@/assets/size-list.json';
import toppings from '@/assets/topping-list.json';

export default {
    name: 'CustomPizza',
    props: {
        pizza: Object
    },
    data() {
        return {
            sizes: sizes.data,
            toppings: toppings.data,
            selectedSize: null,
            selectedToppingIds: [] 
        };
    },
    methods: {
        isAvailable(toppingId) {
            return this.pizza?.toppings?.includes(toppingId);
        },
        emitCustomization() {
            const selectedToppings = this.toppings.filter(t =>
                this.selectedToppingIds.includes(t.id)
            );
            this.$emit('customize', {
                pizza: this.pizza,
                size: this.selectedSize,
                toppings: selectedToppings
            });
        }
    },
    watch: {
  pizza: {
    immediate: true,
    handler(newPizza) {
      // Reset selected toppings based on new pizza availability
      if (Array.isArray(newPizza?.toppings)) {
        this.selectedToppingIds = this.selectedToppingIds.filter(id =>
          newPizza.toppings.includes(id)
        );
      } else {
        this.selectedToppingIds = [];
      }
      this.emitCustomization();
    }
  }
}
};
</script>


<style scoped>
.custom-pizza {
    border-radius: 12px;
    padding-block: 100px;
    color: #333333;
}

.custom-pizza h2 {
    font-size: 32px;
    color: #E77E23;
    margin-bottom: 20px;
}

.custom-section {
    margin-bottom: 20px;
    font-size: 15px;
}

.size-option {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
    font-size: small;
    padding-top: 10px;
}

.radio-label {
    display: flex;
    margin: 0.5rem 0;
    cursor: pointer;
    align-items: center;
}

.extra-price {
    color: gray;
    font-weight: normal;
    margin-left: 4px;
}

.styled-radio {
    accent-color: #f57c00;
    width: 18px;
    height: 18px;
    margin-right: 6px;
    cursor: pointer;
}

.topping-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    margin-top: 1rem;
}

.hidden-checkbox {
    display: none;
}

/* Topping pill style */
.topping-pill {
    font-size: small;
    padding: 8px 16px;
    width: 120px;
    border-radius: 999px;
    border: 1px solid rgb(231, 231, 231);
    text-align: center;
    font-weight: 700;
    cursor: pointer;
    transition: all 0.3s ease;
}

/* Selected topping */
.topping-pill:hover {
    background-color: #ffffff;
    color: #f57c00;
    border-color: #f57c00;
}

.topping-pill.selected {
    background-color: #F8D8BD;
    color: #f57c00;
    border-color: #f57c00;
}

.topping-pill.disabled {
    opacity: 0.4;
    background-color: #E3E3E3;
    cursor: not-allowed;
    color: #6d6d6d;
}
</style>