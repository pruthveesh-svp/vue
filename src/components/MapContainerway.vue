<template>
  
   <div>
    <div class="farmingContent">
      <h2>Farming and Crop Delivery</h2>
      <p  class="line1">
        Farming sustains communities by producing crops and fostering agricultural practices.
        <span class="line1">From the farmer's fields to the customer's table, a robust delivery system ensures</span>
        <span>fresh and quality produce reaches consumers.</span>
      </p>
      <p class="line3">
        Efforts in logistics and distribution, including transportation networks and market
        <span class="line3">accessibility, play a vital role in delivering farm-fresh products promptly and efficiently.</span>
      </p>
      <button @click="getUserLocation">Get Current Location</button>
    </div>
  
    <div ref="map" class="mapContainer"></div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue';
import 'leaflet/dist/leaflet.css';
import L from 'leaflet';

export default {
  setup() {
    const map = ref(null);
    let leafletMap = null;
    const googleMapImageUrl = ref('');

    const googleIcon = L.icon({
      iconUrl: 'https://maps.gstatic.com/mapfiles/api-3/images/spotlight-poi2.png',
      iconSize: [38, 48],
      iconAnchor: [24, 48],
    });

    const getUserLocation = () => {
      if ('geolocation' in navigator) {
        navigator.geolocation.getCurrentPosition(
          (position) => {
            const { latitude, longitude } = position.coords;
            const userCoords = [latitude, longitude];

            if (leafletMap) {
              L.marker(userCoords, { icon: googleIcon }).addTo(leafletMap).bindPopup('Your Location').openPopup();
              leafletMap.setView(userCoords, 13);
            }

            const apiKey = 'YOUR_GOOGLE_MAPS_API_KEY'; // Replace with your actual Google Maps API key
            const imageSize = '400x300';
            const marker = `&markers=color:red%7Clabel:A%7C${latitude},${longitude}`;
            const googleMapImageApiUrl = `https://maps.googleapis.com/maps/api/staticmap?center=${latitude},${longitude}&zoom=13&size=${imageSize}&maptype=roadmap${marker}&key=${apiKey}`;
            googleMapImageUrl.value = googleMapImageApiUrl;
          },
          (error) => {
            console.error('Error getting user location:', error);
          }
        );
      } else {
        console.log('Geolocation is not supported.');
      }
    };

    onMounted(() => {
      if (!map.value) return;

      leafletMap = L.map(map.value).setView([51.505, -0.09], 13);

      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; OpenStreetMap contributors'
      }).addTo(leafletMap);

      onUnmounted(() => {
        leafletMap.remove();
      });
    });

    return { map, getUserLocation, googleMapImageUrl };
  }
};
</script>




<style>
.mapContainer {
  width: 95%;
  height: 500px;
  border: 1px solid #ccc;
  border-radius: 20px;
  margin: 0 auto;
  padding-left: 20px;
  padding-right: 20px;
  margin-bottom: 50px;
}

.farmingContent {
  padding: 16px;
  background-color: #f9f9f9;
  border-radius: 8px;
  margin-top: 16px;
    margin-bottom: 50px;

  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

button {
  margin-bottom: 16px;
  padding: 10px 20px;
  font-size: 1rem;
  border: none;
  border-radius: 5px;
  background-color: #4CAF50;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #45a049;
}
.line1 {
  color: #FF5733; /* Orange */
}

.line2 {
  color: #9B59B6; /* Purple */
}

.line3 {
  color: #3498DB; /* Blue */
}

/* Media query for responsiveness */
@media screen and (max-width: 600px) {
  button {
    padding: 8px 16px;
    font-size: 0.9rem;
  }
}
</style>
