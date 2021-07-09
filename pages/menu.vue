<template>
  <div>
    <section id="gallery">
      <div id="myBtnContainer">
        <button v-for="(category , index) in categories" :key="index" class="btn" :class="category.slug == defaultCat ? 'active': ''" @click="filterSelection(category.slug)">
          {{ category.name }}
        </button>
        <!-- <button class="btn active" @click="filterSelection('mac')">
          Mac N Cheese
        </button>
        <button class="btn" @click="filterSelection('desserts')">
          Desserts
        </button> -->
      </div>

      <!-- Portfolio Gallery Grid -->
      <div class="galleryContainer">
        <div class="row">
          <div v-for="(item , i) in items" :key="i" class="column" :class="item._embedded['wp:term'][0][0].slug">
            <!-- <div class="content">
           
              <img :src="item._embedded['wp:featuredmedia'][0].source_url" alt="Lights" style="width: 100%" />
              <div class="details-section">
                <h4 v-html="item.title.rendered"></h4>
                <p v-if="item.content.rendered" v-html="item.content.rendered">
                 
                </p>
                <span>$ {{ item.metadata.price[0]}}</span>
              </div>
            </div> -->
            <item :item="item"></item>
          </div>
         

       

         
         
          <!-- END GRID -->
        </div>
      </div>
    </section>
  </div>
</template>

<script>

import axios from 'axios';
export default {
  data() {
    return {
      defaultCat: "entree",
      itemsUrl: 'https://unleashedcheese.curotec.net/wp-json/wp/v2/items?_embed&per_page=100',
      categoriesUrl: 'https://unleashedcheese.curotec.net/wp-json/wp/v2/categories',
      items:null,
      categories: null,
    };
  },
  methods: {
    filterSelection(c) {
      this.defaultCat = c;
      var x, i;
      x = document.getElementsByClassName("column");
      if (c == "all") c = "";
      // Add the "show" class (display:block) to the filtered elements, and remove the "show" class from the elements that are not selected
      for (i = 0; i < x.length; i++) {
        this.RemoveClass(x[i], "show");
        if (x[i].className.indexOf(c) > -1) this.AddClass(x[i], "show");
      }
    },
    // Show filtered elements
    AddClass(element, name) {
      var i, arr1, arr2;
      arr1 = element.className.split(" ");
      arr2 = name.split(" ");
      for (i = 0; i < arr2.length; i++) {
        if (arr1.indexOf(arr2[i]) == -1) {
          element.className += " " + arr2[i];
        }
      }
    },
    // Hide elements that are not selected
    RemoveClass(element, name) {
      var i, arr1, arr2;
      arr1 = element.className.split(" ");
      arr2 = name.split(" ");
      for (i = 0; i < arr2.length; i++) {
        while (arr1.indexOf(arr2[i]) > -1) {
          arr1.splice(arr1.indexOf(arr2[i]), 1);
        }
      }
      element.className = arr1.join(" ");
    },
  },
  mounted() {

    axios
      .get(this.categoriesUrl)
      .then( (response) => {
        // handle success

        this.categories = response.data;
       
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      })
      .then( () => {
        // always executed

      });

      axios
      .get(this.itemsUrl)
      .then( (response) => {
        // handle success

        this.items = response.data;
        console.log(this.items)
       
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      })
      .then( () => {
        // always executed
        this.filterSelection(this.defaultCat);

      });


     // Execute the function and show all columns
    console.log('default cat fired')
    // Add active class to the current button (highlight it)
    var btnContainer = document.getElementById("myBtnContainer");
    var btns = btnContainer.getElementsByClassName("btn");
    for (var i = 0; i < btns.length; i++) {
      btns[i].addEventListener("click", function () {
        var current = document.getElementsByClassName("active");
        current[0].className = current[0].className.replace(" active", "");
        this.className += " active";
      });
    }
  },
};
</script>

<style scoped>
#gallery {
  padding-top: 40px;
  height: 100%;
  background-color: #fff8d6;
  text-align: center;
  margin: auto;
}

.row {
  width: 100%;
  margin-left: 10%;
  /* text-align: center; */
  /* margin: 8px -16px; */
}

/* Add padding BETWEEN each column (if you want) */
/* .row, */
.row > .column {
  padding: 8px;
}

/* Create three equal columns that floats next to each other */
.column {
  float: left;
  width: 20%;
  display: none; /* Hide columns by default */
}

/* Clear floats after rows */
.row:after {
  content: "";
  display: table;
  clear: both;
}

/* Content */
.content {
  /* background-color: white;
  padding: 10px; */
}

/* The "show" class is added to the filtered elements */
.show {
  display: block;
}

/* Style the buttons */
.btn {
  border: none;
  outline: none;
  padding: 12px 16px;
  background: none;
  /* background-color: white; */
  font-weight: 800;
  color: #7c2916;
  font-size: 3rem;
  cursor: pointer;
}

/* Add a grey background color on mouse-over */
.btn:hover {
  /* background-color: #ddd; */
}

/* Add a dark background color to the active button */
.btn.active {
  background-color: #f47d23;
  font-weight: 800;
  color: white;
}

#myBtnContainer {
  /* width: 100%; */

  display: flex;
  justify-content: space-around;
  padding: 20px 10%;
}

.galleryContainer {
  display: flex;
  justify-content: center;
}


/* .details-section:hover {
  display: inline;
} */

@media (min-width: 320px) and (max-width: 480px) {
  /* Mobile view */
  .row {
    margin-left: 1%;
  }

  .btn {
  
  font-size: 1rem;
 
}
}



</style>
