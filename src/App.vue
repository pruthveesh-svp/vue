<template>
  <v-app>
    <!-- AppHeaderSection -->
    <v-container fluid>
      <v-row align="center">
        <v-col cols="12">
          <AppHeaderSection />
          <BackGround/>
          <ResponsiveLayout/>
          <GridContent/>
          <GraphDesign/>
          <MapContainerway/>
          <MapContainorGraph/>
          <AppFooterSection/>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import AppHeaderSection from './components/AppHeaderSection.vue';
import BackGround from './components/BackGround.vue';
import GridContent from './components/GridContent.vue';
import ResponsiveLayout from './components/ResponsiveLayout.vue';
import MapContainerway from './components/MapContainerway.vue';
import GraphDesign from './components/GraphDesign.vue';
import MapContainorGraph from './components/MapContainorGraph.vue';
import AppFooterSection from './components/AppFooterSection.vue';






export default {
  components: {
    AppHeaderSection,
    BackGround,
    ResponsiveLayout,
    GridContent,
    GraphDesign,
    MapContainerway,
    MapContainorGraph,
    AppFooterSection
  },
  // Other configurations
};
</script>

<style>
/* Global styles */
body {
  margin: 0;
  font-family: 'Roboto', sans-serif;
}

/* Responsive styles */
/* Adjustments for medium-sized screens */
@media screen and (max-width: 960px) {
  .v-card {
    padding: 2rem;
  }
  .title {
    font-size: 3rem;
  }
  .description {
    font-size: 1.2rem;
  }
}

/* Adjustments for smaller screens */
@media screen and (max-width: 600px) {
  .v-card {
    padding: 1rem;
  }
  .title {
    font-size: 2rem;
  }
  .description {
    font-size: 1rem;
  }
}
</style>
