<template>
  <div class="container">
    <!-- Left side heading -->
    <div class="left-side">
      <h1 class="heading">
        <span class="green-text">Farming</span> and <span class="blue-text">Supply</span>
      </h1>
      <p class="description">
        Exploring the world of agriculture and its supply chain to consumers.
      </p>
    </div>
    <div class="right-side">
      <div class="video-container" @click="toggleAutoplay">
        <video ref="videoPlayer" controls :autoplay="autoplay" muted loop width="480" height="270">
          <source :src="videoSource" type="video/mp4" />
          Your browser does not support the video tag.
        </video>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      videoSource: require('@/assets/v1.mp4'),
      autoplay: true,
    };
  },
  methods: {
    toggleAutoplay() {
      this.autoplay = !this.autoplay;
      const video = this.$refs.videoPlayer;
      if (this.autoplay) {
        video.play();
      } else {
        video.pause();
      }
    },
  },
};
</script>

<style>
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: #f5f5f5;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.left-side {
  flex: 1;
  padding: 20px;
  color: #333;
}

.right-side {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.heading {
  font-size: 3rem;
  margin-bottom: 20px;
}

.green-text {
  color: green;
}

.blue-text {
  color: blue;
}

.description {
  font-size: 1.2rem;
}

.video-container {
  max-width: 100%;
  max-height: 100%;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}


@media screen and (max-width: 768px) {
  .container {
    flex-direction: column;
    align-items: stretch;
  }

  .left-side {
    margin-bottom: 20px;
  }

  .video-container {
    width: 100%;
  }
}
</style>

