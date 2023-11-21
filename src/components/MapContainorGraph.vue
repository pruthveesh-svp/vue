<template>
  <div>
    <div class="farmingContent">
      <h2 class="title">Farming and Agricultural Practices</h2>
      <div class="additionalContent">
        <p class="line1">Agriculture forms the backbone of communities, cultivating crops and fostering sustainable farming methods.</p>
        <p class="line2">Streamlined delivery channels from farmers to consumers guarantee access to fresh, nutrient-rich produce, bolstering healthier lifestyles and backing regional economies.</p>
        <p class="line3">Direct farm-to-consumer supply chains and optimized logistical networks bridge the divide between producers and buyers, ensuring transparent and high-quality food distribution.</p>
        <p class="line4">Granting direct consumer access to farm-fresh goods nurtures a profound comprehension of food origins, promotes sustainability, and fortifies the local agricultural landscape.</p>
      </div>
      <div class="searchSection">
        <input
          type="text"
          placeholder="Search a location"
          v-model="searchQuery"
          @keyup.enter="searchLocation"
          class="searchInput"
        />
        <button @click="searchLocation" class="searchButton">Search</button>
        <button @click="getUserLocation" class="locationButton">Get Current Location</button>
      </div>
    </div>
    <div ref="map" class="mapContainer"></div>
  </div>
</template>

<script>
import { onUnmounted } from 'vue';
import 'leaflet/dist/leaflet.css';
import L from 'leaflet';

export default {
  data() {
    return {
      searchQuery: '',
      leafletMap: null,
    };
  },
  methods: {
    getUserLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition((position) => {
          const { latitude, longitude } = position.coords;
          if (this.leafletMap) {
            this.leafletMap.setView([latitude, longitude], 13);
            L.marker([latitude, longitude])
              .addTo(this.leafletMap)
              .bindPopup('Your Location')
              .openPopup();
          }
        }, (error) => {
          console.error('Error getting user location:', error);
        });
      } else {
        console.error('Geolocation is not supported by this browser.');
      }
    },
  searchLocation() {
  const accessToken = '';
  const query = this.searchQuery;

  fetch(
    `https://api.mapbox.com/geocoding/v5/mapbox.places/${encodeURIComponent(query)}.json?access_token=${accessToken}`
  )
    .then((response) => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then((data) => {
      const features = data.features;

      if (features.length > 0) {
        const [longitude, latitude] = features[0].center;

        if (this.leafletMap) {
          this.leafletMap.setView([latitude, longitude], 13);
          L.marker([latitude, longitude])
            .addTo(this.leafletMap)
            .bindPopup('Searched Location')
            .openPopup();
        }
      } else {
        console.error('No results found for the search query.');
      }
    })
    .catch((error) => {
      console.error('Error fetching location:', error);
    });
},

  },
  mounted() {
    const leafletMap = L.map(this.$refs.map).setView([51.505, -0.09], 13);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; OpenStreetMap contributors',
    }).addTo(leafletMap);

    onUnmounted(() => {
      leafletMap.remove();
    });

    this.leafletMap = leafletMap;
  },
};
</script>

<style scoped>
.mapContainer {
  width: 95%;
  height: 500px;
  border: 1px solid #ccc;
  border-radius: 20px;
  margin: 0 auto;
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
.title {
  color: #F39C12; 
  font-size: 2.5rem; 
  margin-bottom: 20px;
  text-transform: uppercase;
  font-family: 'Arial', sans-serif; 
  text-align: center;
}

.additionalContent {
  margin-bottom: 30px;
}

.line {
  line-height: 1.6;
  font-size: 1.2rem;
  font-family: 'Courier New', monospace;
}

.line.line1 {
  color: #FF5733;
}

.line.line2 {
  color: #9B59B6;
}

.line.line3 {
  color: #3498DB;
}

.line.line4 {
  color: #27AE60; 
}
.searchSection {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
  
}

.searchInput {
  flex: 1;
  margin-right: 10px;
  padding: 6px;
  font-size: 14px;
  width: 150px; /* Adjusted width */
  border: 1px solid #ccc;
  border-radius: 5px;
}


.searchButton,
.locationButton {
  margin-bottom: 16px;
  padding: 10px 20px;
  font-size: 1rem;
  border: none;
  border-radius: 5px;
  background-color: #4caf50;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.searchButton:hover,
.locationButton:hover {
  background-color: #45a049;
}

@media screen and (max-width: 600px) {
  .searchButton,
  .locationButton {
    padding: 8px 16px;
    font-size: 0.9rem;
  }
}
</style>
