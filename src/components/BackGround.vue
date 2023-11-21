<template>
  <v-container
    class="farming-section"
    :style="{ backgroundImage: `url(${backgroundImage})`, color: textColor, marginTop: '40px', display: 'flex', flexDirection: 'column', justifyContent: 'center', alignItems: 'center' }"
    fluid
  >
    <v-row>
      <v-col cols="12" class="text-center">
        <h1 :class="titleClasses" @mouseover="applyHoverEffect('title')" @mouseleave="removeHoverEffect('title')">
          Farming and Agriculture
        </h1>
        <p :class="descriptionClasses" @mouseover="applyHoverEffect('description')" @mouseleave="removeHoverEffect('description')">
          Exploring sustainable farming practices and the journey from farm to table.
        </p>
        <div class="button-container">
          <button class="change-background-btn" @click="changeBackgroundImage(require('@/assets/Banner2.jpg'))">Change Background</button>
          <button class="mode-toggle-btn" @click="toggleDarkMode">Toggle Dark/Light Mode</button>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      backgroundImage: require('@/assets/banner.jpg'),
      textColor: '#fff', // Default text color
    };
  },
  computed: {
    titleClasses() {
      return {
        fontSize: '3rem',
        '@media (max-width: 600px)': {
          fontSize: '2rem',
        },
      };
    },
    descriptionClasses() {
      return {
        fontSize: '1.5rem',
        '@media (max-width: 600px)': {
          fontSize: '1rem',
        },
      };
    },
  },
  methods: {
    changeBackgroundImage(newImage) {
      this.backgroundImage = newImage;
    },
    toggleDarkMode() {
      if (this.textColor === '#fff') {
        this.textColor = '#000'; // Change to dark text color
       
      } else {
        this.textColor = '#fff'; // Change back to light text color
      }
    },
    applyHoverEffect(element) {
      if (element === 'title') {
        this.titleClasses.fontSize = '3.5rem';
      } else if (element === 'description') {
        this.descriptionClasses.fontSize = '1.8rem';
      }
    },
    removeHoverEffect(element) {
      if (element === 'title') {
        this.titleClasses.fontSize = '3rem';
      } else if (element === 'description') {
        this.descriptionClasses.fontSize = '1.5rem';
      }
    },
  },
};
</script>

<style scoped>
.farming-section {
  background-size: cover;
  background-position: center;
  height: 100vh;
  display: flex;
  align-items: center;
  color: #fff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.8);
  border-radius: 20px; 
  overflow: hidden; 
}

.title {
  font-size: 3rem;
  margin-bottom: 20px;
}

.description {
  font-size: 1.5rem;
  opacity: 0.9;
}

.button-container {
  margin-top: 20px;
}

.change-background-btn,
.mode-toggle-btn {
  padding: 10px 20px;
  margin: 0 10px;
  border: none;
  border-radius: 5px;
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.change-background-btn {
  background-color: #3498db;
  color: #fff;
}

.mode-toggle-btn {
  background-color: #e74c3c;
  color: #fff;
}

.change-background-btn:hover,
.mode-toggle-btn:hover {
  background-color: #2980b9;
}
</style>
