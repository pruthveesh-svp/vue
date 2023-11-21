<template>
  <div class="container1">
    <h1>
      <span class="farmers">Farmers</span>
      <span class="market">Market</span>
    </h1>
  </div>
  <div class="container">
    
    <div v-for="(_, index) in products" :key="index" class="product">
      <img :src="getImageSource(products[index].image)" :alt="products[index].name" class="product-image" />
      <div class="product-details">
        <h2>{{ products[index].name }}</h2>
        <p>Price: Rs{{ products[index].price }}</p>
        <p>Available Quantity: {{ products[index].quantity }}</p>
        <!-- Input for customer order -->
        <div v-if="products[index].quantity > 0">
          <label for="orderQty">Order Quantity:</label>
          <input type="number" v-model="orderQuantities[index]" min="0" :max="products[index].quantity" />
          <button @click="placeOrder(index)">Place Order</button>
        </div>
      </div>
      <hr class="divider" />
    </div>
    <h2>Market Price Details</h2>
    <p v-if="marketPrice">Market Price for {{ marketProduct }}: Rs{{ marketPrice }}</p>
    <p v-else>No market price available for {{ marketProduct }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { name: 'Apples', price: 25, quantity: 50, image: require('@/assets/apple.jpg') },
        { name: 'Oranges', price: 30, quantity: 30, image: require('@/assets/orrage.jpg')  },
        { name: 'Bananas', price: 40, quantity: 20, image: require('@/assets/tomato.jpg')  },
        { name: 'Grapes', price: 50, quantity: 25, image: require('@/assets/papaya.jpg')  },
      ],
      orderQuantities: [], 
      marketProduct: 'Apples', 
      marketPrice: 0 
    };
  },
  methods: {
    placeOrder(index) {
      const orderedQuantity = this.orderQuantities[index];
      if (orderedQuantity > 0 && orderedQuantity <= this.products[index].quantity) {
        const totalPrice = orderedQuantity * this.products[index].price;

        this.products[index].quantity -= orderedQuantity;

        alert(`Order placed for ${orderedQuantity} ${this.products[index].name} for a total of $${totalPrice}`);

        this.orderQuantities[index] = 0;
      } else {
        alert('Invalid quantity or not enough in stock!');
      }
    },
    fetchMarketPrice() {
      
      this.marketPrice = Math.random() * 10; 
    },
    getImageSource(image) {
    
      if (image.startsWith('@/assets/')) {
        return require(`@/${image}`);
      } else {
        return image;
      }
    }
  },
  created() {
    this.fetchMarketPrice();
  }
};
</script>

<style scoped>
.container {
  width: 100vw;
  padding: 20px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 20px;
    text-align: center;

  background-color: #f7f7f7;
  overflow-y: auto;
}
.container1 {
    text-align: center;
 
}

.product {
  width: calc(25% - 20px);
  min-width: 200px;
  background-color: #fff;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.product:hover {
  transform: translateY(-5px);
}

.product-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
  transition: filter 0.3s ease;
}

.product:hover .product-image {
  filter: brightness(80%);
  margin-bottom: 20px;
}

.product-details {
  padding: 20px;
  margin-bottom: 20px;
}

.product h2 {
  font-size: 1.2rem;
  margin-bottom: 20px;
}

.product p {
  margin-bottom: 8px;
}

.product button {
  padding: 8px 16px;
  border: none;
  margin-top: 20px;
  background-color: #3498db;
  color: #fff;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.product button:hover {
  background-color: #2980b9;
}

.divider {
  width: 100%;
  margin-top: 10px;
  border-top: 1px solid #ccc;
}
.farmers {
  color: #ff6347; 
}

.market {
  color: #4682b4; 
}
</style>

