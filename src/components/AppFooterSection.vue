<template>
  <footer class="footer">
    <div class="footer-content">
      <div class="social-media">
        <a href="https://twitter.com" target="_blank"><i class="fab fa-twitter"></i></a>
        <a href="https://facebook.com" target="_blank"><i class="fab fa-facebook"></i></a>
        <!-- Add more social media icons or links -->
      </div>
      <div class="footer-box">
        <p>© 2023 Farming Co. All Rights Reserved</p>
        <div class="footer-links">
          <router-link to="/">Contact us: farmingco@example.com | Phone: 123-456-7890</router-link>
          <a href="#" @click="openContactModal">Live Chat</a>
        </div>
      </div>
    </div>
   </footer>
</template>

<style scoped>
.footer {
  background-color: #333;
  color: #fff;
  padding: 20px 0;
}

.footer-content {
  display: flex;
  justify-content: center; 
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
}

.footer-box {
  padding: 20px;
  border: 1px solid #555;
  border-radius: 5px;
}

.footer-box p {
  margin: 0;
}

.footer-links a {
  color: #fff;
  margin-right: 10px;
  text-decoration: none;
}

.social-media a {
  color: #fff;
  margin: 0 5px;
  font-size: 20px;
}



</style>
