<template>
  <v-app>
    <v-container fluid>
      <v-row>
        <v-col cols="12">
          <div class="header" :class="{ 'sticky': isSticky }">
            <div class="title-box" :style="titleBoxStyles">
              <h1 :class="titleClasses">
                Farming and Crop Delivery
              </h1>
            </div>
            <nav class="navbar">
              <div class="logo">
                <!-- Your logo or site title -->
                <h1 :class="titleClasses">FreshFarm</h1>
              </div>
              <div class="menu-toggle" @click="toggleMenu">
                <!-- Menu icon or text -->
                <i class="fas fa-bars"></i> <!-- Assuming you're using Font Awesome for icons -->
              </div>
              <ul :class="{ 'active': isMenuOpen }" class="menu">
               <li><a href="#" class="box-link">Home</a></li>
                <li><a href="#" class="box-link">About</a></li>
                <li><a href="#" class="box-link">Services</a></li>
                <li><a href="#" class="box-link">Contact</a></li>
              </ul>
            </nav>
          </div>
        </v-col>
      </v-row>
      <!-- Your main content here -->
      <!-- ... -->
    </v-container>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      isMenuOpen: false,
      isSticky: false
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    handleScroll() {
      if (window.scrollY > 100) {
        this.isSticky = true;
      } else {
        this.isSticky = false;
      }
    }
  },
  computed: {
    titleClasses() {
      return {
        'text-h1': true,
        'font-weight-bold': true,
         'rainbow-text': true
      };
    },
    titleBoxStyles() {
      return this.isSticky ? { backgroundColor: '#333', color: '#fff' } : {};
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll);
  }
};
</script>

<style scoped>
.header {
  width: 100%;
  transition: background-color 0.3s ease-in-out;
  position: relative;
  z-index: 1000;
}

.sticky {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.title-box {
  padding: 20px;
  transition: background-color 0.3s ease-in-out, color 0.3s ease-in-out;
}

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 24px;
}

.menu-toggle {
  display: none; 
  cursor: pointer;
}

.rainbow-text {
  background-image: linear-gradient(to right, violet, indigo, blue, green, yellow, orange, red);
  -webkit-background-clip: text;
  color: transparent;
}
.menu {
  display: flex;
  list-style: none;
  padding: 0;
}

.menu li {
  margin-right: 20px;
}

.menu a {
  text-decoration: none;
  color: #333;
  transition: color 0.3s ease-in-out;
}

.menu a:hover {
  color: #ff0000;
}
.box-link {
  display: block;
  padding: 10px 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-right: 10px;
  transition: background-color 0.3s ease-in-out, color 0.3s ease-in-out;
}

.box-link:hover {
  background-color: #f9f9f9;
  color: #fff;
}

@media screen and (max-width: 768px) {
  .menu {
    display: none;
    flex-direction: column;
    text-align: center;
    position: absolute;
    top: 60px;
    left: 0;
    width: 100%;
    background-color: #333;
    padding: 10px 0;
  }

  .menu.active {
    display: flex;
  }

  .menu li {
    margin-right: 0;
    margin-bottom: 10px;
  }

  .menu-toggle {
    display: block;
  }
}
</style>
