<template>
  <div class="grid-container">
    <div
      v-for="(data, index) in imagesData"
      :key="index"
      class="grid-item"
      :style="{ marginBottom: '30px', borderRadius: '10px' }"
      @mouseover="showOverlay(index)"
      @mouseleave="hideOverlay"
    >
    
      <img
        :src="data.imageUrl"
        :alt="`Image ${index + 1}`"
        class="image"
        :style="{ borderRadius: '8px' }"
      />
      <div
        v-if="hoveredIndex === index"
        class="overlay"
        :style="{ borderRadius: data.overlayBorderRadius }"
      >
        <h6 class="overlay-text">{{ data.text }}</h6>
        <button @click="toggleOverlay(index)">{{ data.showOverlay ? 'Hide Overlay' : 'Show Overlay' }}</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hoveredIndex: -1,
      imagesData: [
        {
          imageUrl: require('@/assets/download.jpg'),
          text: 'Farming forms the backbone of food production, supplying essential nourishment to communities worldwide.',
          showOverlay: false,
          overlayBorderRadius: '8px',
        },
        {
          imageUrl: require('@/assets/download1.jpg'),
          text: 'It plays a pivotal role in environmental conservation, fostering biodiversity, soil health, and sustainable land management practices.',
          showOverlay: false,
          overlayBorderRadius: '8px',
        },
        {
          imageUrl: require('@/assets/download2.jpg'),
          text: 'Farming serves as an economic lifeline, providing livelihoods, fostering rural development, and contributing significantly to global economies.',
          showOverlay: false,
          overlayBorderRadius: '8px',
        },
      ],
    };
  },
  methods: {
    showOverlay(index) {
      this.hoveredIndex = index;
    },
    hideOverlay() {
      this.hoveredIndex = -1;
    },
    toggleOverlay(index) {
      this.imagesData[index].showOverlay = !this.imagesData[index].showOverlay;
    },
  },
};
</script>


<style scoped>

.grid-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.grid-item {
  position: relative;
  width: calc(33.33% - 10px);
  transition: all 0.3s ease-in-out;
  margin-top: 20px; 
}

.grid-item:hover .overlay {
  opacity: 1;
}

.image {
  width: 100%;
  height: auto;
  display: block;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
}

.overlay-text {
  color: #fff;
  text-align: center;
  padding: 12px;
}
</style>


