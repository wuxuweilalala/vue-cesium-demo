<template>
  <div class="home">
    <div id="map" >
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',
  mounted() {
    this.mapInit();
  },
  methods:{
    mapInit(){
      const viewer = new Cesium.Viewer('map')
      const numberOfBalloons = 13;
      const lonIncrement = 0.00025;
      const initialLon = -122.99875;
      const lat = 44.0503706;
      const height = 100;
      const url = 'http://192.168.1.242:3000/model/CesiumAir/Cesium_Air.glb';
      for (let i = 0; i < numberOfBalloons; ++i) {
        let lon = initialLon + i * lonIncrement;
        createModel(url, lon, lat, height);
      }
      const target = Cesium.Cartesian3.fromDegrees(initialLon + lonIncrement, lat, height + 7.5);
      const offset = new Cesium.Cartesian3(-37.048378684557974, -24.852967044804245, 4.352023653686047);
      viewer.scene.camera.lookAt(target, offset);
      function createModel(url, x, y, height) {
        const position = Cesium.Cartesian3.fromDegrees(x, y, height);
        viewer.entities.add({
          name : url,
          position : position,
          model : {
            uri : url
          }
        });
      }
    }
  }
}
</script>
