<template>
<div>
  <!-- <div class="content" @mouseover="active = true" @mouseleave="active = false"> -->
    <img
      :src="item._embedded['wp:featuredmedia'][0].source_url"
      alt="Lights"
      style="width: 100%"
    />
    <div class="details-section" v-show="active">
        <div class="triangle-up"></div>
      <h4 v-html="item.title.rendered"></h4>
      <p v-if="item.content.rendered" v-html="item.content.rendered"></p>
      <span>$ {{ item.metadata.price[0] }}</span>
    </div>
  </div>
</template>
<script>
export default {
  props: ["item"],
  data() {
    return {
      active: false,
    };
  },
  methods: {
    mouseOver: function () {
      this.active = !this.active;
    },
  },
};
</script>
<style scoped>

@media (min-width: 320px) and (max-width: 480px) {
.details-section > h4 {
  font-size: 1.2rem !important;
  font-weight: 900;
}
.details-section > p {
  font-size: 1rem !important;
  font-style: italic;
  font-weight: 600;
}

.details-section > span {
  font-size: 1.2rem !important;
  font-weight: 700;
}

}

.triangle-up {
  position: absolute;
  right: 10%;
  top: -40px;
  width: 0;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 50px solid #F47D23ed;
}
.content {
  position: relative;
  cursor: pointer;
}

.details-section {
  /* display: none; */
  position: relative;
  top: 0;
  z-index: 999;
  widows: 100%;
  background: #f47d23;
  color: white;
  text-align: center;
  padding: 10px;
  
}

.details-section > h4 {
  font-size: 3rem;
  font-weight: 900;
}
.details-section > p {
padding-top: 10px;
padding-bottom: 10px;
  font-size: 1.2rem;
  font-style: italic;
  font-weight: 600;
}

.details-section > span {

  font-size: 1.5rem;
  font-weight: 700;
}
</style>