<template>
  <div>
    <section id="hero-section">
      <div class="right-section">
        <h1>it's off<br />the chain</h1>
        <p>
          gourmet Macaroni & Cheese <br />
          delivered straight to your door
        </p>
        <!-- <a href="/order" class="button">order now</a> -->
        <nuxt-link to="/order" class="button" exact>order now</nuxt-link>
      </div>
    </section>

    <section id="first-section">
      <div class="left-side">
        <p>we take<br />cheese <br />seriously</p>
      </div>
    </section>

    <section id="slider-section">
      <div class="slideshow-container">
        
        
        <div v-for="(slider , index ) in sliders" :key="index"  class="mySlides fade">
         
          <img :src="slider._embedded['wp:featuredmedia'][0].source_url" style="width: 100%" />
          <div class="text">
            <h1 v-html="slider.title.rendered"></h1>
            <p v-html="slider.content.rendered">
         
            </p>
            <nuxt-link to="/menu" class="slider-button" exact=""
              >see the menu</nuxt-link
            >
          </div>
        </div>

     
       

        <a class="prev" @click="plusSlides(-1)"
          ><img src="/assets/prev.png"
        /></a>
        <a class="next" @click="plusSlides(1)"
          ><img src="/assets/next.png"
        /></a>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      slideIndex: 1,
      sliders: null,
    };
  },
  methods: {
    plusSlides(n) {
      this.showSlides((this.slideIndex += n));
    },
    currentSlide(n) {
      this.showSlides((this.slideIndex = n));
    },
    showSlides(n) {
      var i;
      var slides = document.getElementsByClassName("mySlides");
      // var dots = document.getElementsByClassName("dot");
      if (n > slides.length) {
        this.slideIndex = 1;
      }
      if (n < 1) {
        this.slideIndex = slides.length;
      }
      for (i = 0; i < slides.length; i++) {
        slides[i].style.display = "none";
      }
      // for (i = 0; i < dots.length; i++) {
      //   dots[i].className = dots[i].className.replace(" active", "");
      // }

      slides[this.slideIndex - 1].style.display = "block";

      //   dots[slideIndex-1].className += " active";
    },
  },

  mounted() {
    
    axios
      .get("https://unleashedcheese.curotec.net/wp-json/wp/v2/slider?_embed")
      .then( (response) => {
        // handle success
        console.log('Sliders data')
        this.sliders = response.data;
       
        
        console.log(this.sliders);
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      })
      .then( () => {
        // always executed

         this.showSlides(this.slideIndex);
      });

     

      
  },

  // watch:{
  //   sliders(oldValue,newValue){
  //     if(oldValue != null){
  //       //  this.showSlides(this.slideIndex);
  //     }
  //   }
  // }
};
</script>

<style scoped>
#hero-section {
  background-image: url("/assets/hero.png");
  background-repeat: no-repeat;
  background-size: cover;
  height: 90vh;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.right-section {
  text-align: right;
  position: relative;
  width: 40%;
  padding-right: 13%;
  /* background: red; */
  font-family: "Montserrat", sans-serif;
  font-weight: 500;
  font-size: 2rem;
  color: #7c2916;
}

.right-section h1 {
  font-weight: 900;
  font-size: 6rem;
}

.right-section p {
  font-style: italic;
  font-weight: 600;
  padding-bottom: 30px;
}

.button {
  background: #7c2916;
  color: white;
  font-weight: 700;
  padding: 5px 50px 5px 50px;
  border-radius: 5px;
  text-decoration: none;
}

#first-section {
  background-image: url("/assets/section1.jpg");
  background-size: cover;
  height: 60vh;
  display: flex;
  align-items: center;
}

#first-section p {
  font-weight: 900;
  font-size: 5rem;
  color: white;
  padding-left: 70px;
}

/* Slider */

.mySlides {
  display: none;
}

.mySlides img {
  vertical-align: middle;
  height: 100vh;
}

/* Slideshow container */

.slideshow-container {
  width: 100%;
  position: relative;
  /* margin: auto; */
}

/* Next & previous buttons */

.prev,
.next {
  cursor: pointer;
  position: absolute;
  top: 50%;
  /* width: auto; */
  /* padding: 16px; */
  /* margin-top: -22px; */
  /* color: white; */
  /* font-weight: bold; */
  /* font-size: 18px; */
  transition: 0.6s ease;
  border-radius: 0 3px 3px 0;
  user-select: none;
}

/* Position the "next button" to the right */

.next {
  right: 5%;
  /* border-radius: 3px 0 0 3px; */
}

.prev {
  left: 5%;
}

/* On hover, add a black background color with a little bit see-through */

/* .prev:hover, .next:hover {
  background-color: rgba(0,0,0,0.8);
} */

/* Caption text */

.text {
  color: #f2f2f2;
  /* font-size: 15px; */
  /* padding: 8px 12px; */
  position: absolute;
  top: 0;
  /* top: 30%; */
  /* bottom: 8px; */
  width: 100%;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background: linear-gradient(rgba(0, 130, 170, 0), rgba(124, 41, 22, 1));
  height: 100vh;
}

.text h1 {
  font-weight: 900;
  font-size: 5rem;
}

.text p {
  font-weight: 700;
  font-size: 1.8rem;
  font-style: italic;
  padding-bottom: 30px;
}

.text .slider-button {
  text-decoration: none;
  color: white;
  background: #f57f23;
  padding: 10px 40px;
  border-radius: 5px;
  font-weight: 700;
  font-size: 2rem;
}

/* Number text (1/3 etc) */

/* .numbertext {
  color: #f2f2f2;
  font-size: 12px;
  padding: 8px 12px;
  position: absolute;
  top: 0;
} */

/* The dots/bullets/indicators */

/* .dot {
  cursor: pointer;
  height: 15px;
  width: 15px;
  margin: 0 2px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
  transition: background-color 0.6s ease;
}

.active, .dot:hover {
  background-color: #717171;
} */

/* Fading animation */

.fade {
  -webkit-animation-name: fade;
  -webkit-animation-duration: 1.5s;
  animation-name: fade;
  animation-duration: 1.5s;
}

.social {
  display: flex;
}

@-webkit-keyframes fade {
  from {
    opacity: 0.4;
  }
  to {
    opacity: 1;
  }
}

@keyframes fade {
  from {
    opacity: 0.4;
  }
  to {
    opacity: 1;
  }
}

/* On smaller screens, decrease text size */

@media only screen and (max-width: 300px) {
  /* .prev, .next,.text {font-size: 11px} */
}

#footer {
  padding: 20px 0px;
  width: 100%;
  /* height: 110px; */
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 25px;
}

#footer span {
  font-weight: 500;
  font-size: 1.2rem;
}

#footer a img {
  width: 80%;
}

@media (min-width: 320px) and (max-width: 480px) {
  /* CSS */

  #hero-section {
    background-size: cover;
    background-position-x: 85%;
    align-items: center;
    height: 100%;
    padding: 60px 0px;
  }
  .right-section {
    text-align: center;
    padding: 0px;
    margin: 0px;
    width: 100%;
  }
  #first-section p {
    font-weight: 900;
    font-size: 3rem;
    color: white;
    text-align: center;
    padding: 0px;
  }
  .left-side {
    width: 100%;
    text-align: center;
  }
  .mySlides img {
    vertical-align: middle;
    height: auto;
  }
  .text {
    height: 100%;
  }
  .text h1 {
    /* font-weight: 900; */
    font-size: 2rem;
  }
  .text p {
    font-weight: 700;
    font-size: 1rem;
    font-style: italic;
    padding-bottom: 10px;
    width: 70%;
  }
  .prev,
  .next {
    cursor: pointer;
    position: absolute;
    top: 20%;
    /* padding: 16px; */
    /* margin-top: -22px; */
    color: white;
    font-weight: bold;
    /* font-size: 18px; */
    transition: 0.6s;
    transform: scale(0.3, 0.3);
    /* user-select: none; */
  }
  .next {
    right: 0%;
    /* border-radius: 3px 0 0 3px; */
  }
  .prev {
    left: 0%;
  }
  .text .slider-button {
    text-decoration: none;
    color: white;
    background: #f57f23;
    padding: 10px 40px;
    border-radius: 5px;
    font-weight: 700;
    font-size: 1rem;
  }
  .right-section h1 {
    font-size: 3rem;
  }

  .row {
    margin-left: 0% !important;
  }
}
</style>
