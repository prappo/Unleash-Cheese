<template>
  <div>
    <nav>
      <div id="brand">
        <a style="display:flex; gap:15px;text-decoration:none;align-items:center" href="/">
        <img id="logo" src="assets/logo.png" />
        <h1 id="brand-name">Unleash Cheese</h1>
        </a>
      </div>

      <div id="menu">
          <nuxt-link to="/" exact>home</nuxt-link> <span></span>
          <nuxt-link to="/menu" exact>menu</nuxt-link> <span></span>
          <nuxt-link to="/order" exact>order</nuxt-link>
        <!-- <a class="selected" href="/">home</a> <span></span>
        <a href="/menu">menu</a> <span></span>
        <a href="/order">order</a> -->
      </div>
    </nav>
    <Nuxt />

    <section id="footer">
      <div class="social">
        <a href="#"><img src="/assets/facebook.png" /></a>
        <a href="#"><img src="/assets/instagram.png" /></a>
        <a href="#"><img src="/assets/twitter.png" /></a>
        <a href="#"><img src="/assets/email.png" /></a>
      </div>
      <img class="footerImage" src="/assets/footerl.png" />
      <span>©2021 Unleash Cheese. All Rights reserved.</span>
    </section>
  </div>
</template>

<style>
* {
  padding: 0px;
  margin: 0px;
  font-family: "Montserrat", sans-serif;
}

body {
  position: absolute;
  width: 100%;
}

section {
  width: 100%;
}

nav {
  display: flex;
  /* width: 100%; */
  padding: 25px 80px 25px 80px;
  /* background-color: blanchedalmond; */
  justify-content: space-between;
}

#logo {
  width: 70px;
}

#brand {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15px;
 
}

#brand-name {
  font-weight: 400;
  font-size: 2.5rem;
  color: #7c2916;
}

#menu {
  display: flex;
  gap: 15px;
  align-items: center;
  /* background-color: burlywood; */
  padding: 0px 10px 0px 10px;
}

#menu a {
  font-family: "Montserrat", sans-serif;
  font-weight: 500;
  font-size: 2rem;
  color: #7c2916;
  text-decoration: none;
}

.selected {
  font-weight: 800 !important;
}

.nuxt-link-active {
    font-weight: 800 !important;
}

#menu span {
  background-color: #7c2916;
  width: 2.5px !important;
  height: 30px;
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

.social {
  display: flex;
}

@media (min-width: 320px) and (max-width: 480px) {
nav {
    display: flex;
    flex-direction: column;
    padding: 20px 0px;
  }
  #brand {
    display: flex;
    flex-direction: column;
  }
  
  #menu {
    margin-top: 10px;
  }
  section {
    width: 100%;
  }

  #footer {
    flex-direction: column;
    text-align: center;
  }
  .footerImage {
    display: none;
  }

}
</style>