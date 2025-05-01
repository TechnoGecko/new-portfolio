<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)
</script>

<template>
  <div id="main-wrapper">
    <div id="nav">
      <!-- TODO -->
    </div>
    <div id="side-by-side-main">
      <div id="left-section-main">
        <h1 id="namecard">Cody <img id="namecard-img" src="../../assets/CodyPortfolioAnim.gif" /><br /> Reeves</h1>
        <div id="lower-section">
          <div id="rotating-title-container">
            <div id="title-top-divider"></div>
            <h2 id="rotating-title">Full Stack Developer</h2>
          </div>
          <div id="rotating-text-container">
            <div id="title-side-divider"></div>
            <p id="rotating-text">Some text about the current title that expands on it, and sells my skills a little
              bit.
            </p>
          </div>
        </div>
      </div>
      <div id="right-section-main">
        <h1 style="font-size: 123px;">FUCK<br /> FDG<br /> BRO</h1>
      </div>
    </div>
  </div>
</template>

<style scoped>
#main-wrapper {
  display: flex;
  flex-direction: column;
  margin: 0;
  padding: 0;
}

#side-by-side-main {
  display: flex;

}

#namecard {
  font-size: 124px;
  font-family: "Roboto Serif", serif;
  font-style: italic;
  text-transform: uppercase;
  font-weight: 100;
  width: 100%;
}


#rotating-title {
  font-family: "Roboto Serif", serif;
  font-weight: 200;
}

#rotating-title {
  font-weight: 200;
}

#rotating-text {
  font-family: "Josefin Slab", serif;
  font-size: 24px;
  font-weight: 100;
  font-style: italic;
  color: #a2a2a2;
}

#rotating-text-container {
  display: flex;
  gap: 21px;
}

#left-section-main,
#right-section-main {
  margin: 20px 2vw;
  width: calc(50% - 2vw);
}

#right-section-main {
  display: flex;
  justify-content: center;
  border-left: 1px solid #c2c2c2;
}

#lower-section {
  display: flex;
  gap: 22px;
}

#namecard-img {
  width: 150px;
  height: 150px;
}

#title-top-divider {
  display: block;
  width: 100%;
  height: 0px;
  border-top: 1px solid #c2c2c2;
}

#title-side-divider {
  display: block;
  height: 100%;
  width: 0px;
  border-right: 1px solid #d2d2d2;
}
</style>
