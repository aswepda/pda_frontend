<script>
import GPSLocation from "../Location";
export default {
  methods: {
    async getDirection(dest, mode, lat = null, lon = null) {
      if (!lat || !lon) {
        var location = await this.requestLocation();
        lat = location.coords.latitude;
        lon = location.coords.longitude;
      }
      let dirData = await this.$http.get(
        `directions/${lat},${lon}/${mode}/${dest}`
      );
      return dirData.data.data;
    },
    parseDirectionText(direction) {
      switch(direction) {
        case "driving":
          return "mit dem Auto";
        case "walking":
          return "zu Fuß";
        case "transit":
          return "mit ÖPNV";
        case "bicycling":
          return "mit dem Fahrrad"
      }
    },
  },
  mixins: [GPSLocation],
};
</script>