<template>
  <div>
    <section id="order-section">
      <div class="location-container">
        <div class="location">
          <span>your location</span>
          <select v-model="selected">
            <option
              v-for="(location, index) in locations"
              :key="index"
              :value="location.id"
            >
              {{ location.title.rendered }}
            </option>
          </select>
        </div>

        <div class="provider-wraper">
          <div class="provider-container">
            <div id="grubhub">
              <img src="assets/grubhub.png" />
            </div>

            <div id="doordash">
              <img src="assets/doordash.png" />
            </div>
          </div>

          <div id="providerBtnContainer">
            <button @click="goGH" class="btnProvider">go!</button>
            <button @click="goDD" class="btnProvider">go!</button>
          </div>
        </div>
      </div>

      <div class="qoute">
        <h1>cheesed to meet you.</h1>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      locations: null,
      selected: null,
      locationsURL: "https://unleashedcheese.curotec.net/wp-json/wp/v2/locations",
    };
  },
  methods: {
    goGH() {
      if (this.selected) {
        var url = "";
        for (const index in this.locations) {
          var location = this.locations[index];
          if (location.id == this.selected) {
            url = location.metadata.gh;
          }
        }
        console.log(url[0]);

        window.open(url, "_blank").focus();
      }
    },

    goDD() {
      if (this.selected) {
        var url = "";
        for (const index in this.locations) {
          var location = this.locations[index];
          if (location.id == this.selected) {
            url = location.metadata.dd;
          }
        }
        console.log(url[0]);

        window.open(url, "_blank").focus();
      }
    },
  },
  mounted() {
    axios
      .get(this.locationsURL)
      .then((response) => {
        this.locations = response.data;
        this.selected = response.data[0].id;
      })
      .catch(function (error) {
        console.log(error);
      })
      .then(() => {});
  },
};
</script>

<style scoped>
#order-section {
  height: 150vh;
  background-image: url("/assets/bgorder.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-color: #fff8d6;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.provider-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 30px;
}

.provider-wraper {
  padding: 30px;
  background-color: #fff8d6;
  border: 8px solid #7c2916;
}

#providerBtnContainer {
  padding-top: 20px;
  display: flex;
  justify-content: space-around;
}

.btnProvider {
  background: #7c2916;
  border: none;
  color: white;
  font-weight: 700;
  font-size: 3rem;
  width: 40%;
  border-radius: 10px;
  cursor: pointer;
}

.location {
  padding-bottom: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
}

.location span {
  color: #7c2916;
  font-weight: 600;
  font-style: italic;
  font-size: 2rem;
}

.location select {
  background-color: #7c2916;
  color: white;
  border-radius: 10px;
  font-size: 3rem;
  font-weight: 600;
  padding: 5px 30px;
}

#grubhub {
  display: flex;
  flex-direction: column;
}

#doordash {
  display: flex;
  flex-direction: column;
}

.qoute {
  margin-top: 20%;
  font-weight: 900;
  color: #7c2916;
  font-size: 3rem;
}

@media (min-width: 320px) and (max-width: 480px) {
  .location-container {
    width: 100%;
  }

  #grubhub > img {
    width: 100%;
  }

  #doordash > img {
    width: 100%;
  }

  .btnProvider {
    font-size: 2rem;
  }

  .location select {
    font-size: 2rem;
  }

  .location span {
    font-size: 1.2rem;
  }

  .qoute {
    font-size: 2rem;
    text-align: center;
  }

  #order-section {
    height: 90vh;
  }
}
</style>
