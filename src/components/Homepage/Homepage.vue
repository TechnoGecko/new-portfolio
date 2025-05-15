<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import '../../style.css'

const userHasScrolled = ref(false);
const namecardHasMoved = ref(false);
const currentSlideshowStep = ref(0);
const inputDelayIsActive = ref(false);
const inputDelayLengthMs = 1500;


const slideshowSteps = [
  {
    "title": "Full Stack Developer",
    "subtitle": "I excel in a wide range of web technologies, from interactive UIs to complex database architecture and ",
    "sections": [],
  },
  {
    "title": "Agency Experience",
    "subtitle": "With 2 years of agency experience using a wide range of technologies and adressing an even wider variety of client needs, I'm adaptable and intuitive when searching for solutions to tricky problems.",
    "sections": [
      {
        "title": "PHP and SQL",
        "subtitle": "A full-stack web development match made in heaven, once you get used to the syntax!"
      },
      {
        "title": "Javascript and Friends",
        "subtitle": "I often prefer vanilla JS when I have the choice, but I'm just as comfortable in a framework like React or Vue.",
      },
      {
        "title": "Shopify and Ruby",
        "description": "I have experience making customizations to shopify themes, from visual edits to full functionality overhauls. Writing custom apps and scripts."
      }
    ],
    "section_id": ""
  },
  {
    "title": "Personal Projects",
    "subtitle": "Programming has also found it's way into my creative life. Game and app development turned out to be a convergance of the many seemingly-unrelated hobbies I've picked up throughout my life, and learning to code was just the missing piece.",
    "sections": [''],
    "section_id": ""
  },
]

onMounted(() => {
  const listenForInitialScrollorClick = (e) => {
    if (inputDelayIsActive.value == true) return;
    if (e.deltaY > 0 || e.type == 'click') {
      userHasScrolled.value = true; // Toggle reactive flag
      namecard.style.minWidth = '425px';
      namecard.style.transition = 'color .15s ease-in';
      namecard.style.color = 'rgba(0,0,0,0)';
      startInputDelay();
      // namecard.querySelector('#namecard-img').style.display = 'none';
      setTimeout(() => {
        modifyNamecardForHeader();
        namecardHasMoved.value = true;
      }, 300)

      window.removeEventListener('wheel', listenForInitialScrollorClick);
      window.removeEventListener('click', listenForInitialScrollorClick);
      window.addEventListener('wheel', listenForSlideshowScrollOrClick);
      window.addEventListener('click', listenForSlideshowScrollOrClick);
    }
  }

  const modifyNamecardForHeader = () => {
    let namecard = document.getElementById('namecard');
    namecard.style.color = 'unset';
    namecard.appendChild(document.getElementById('namecard-img'));
    document.querySelector('#namecard>br').remove();
    namecard.querySelector('#namecard-img').style.display = 'unset';
    namecard.style.margin = 0;
  }


  const listenForSlideshowScrollOrClick = () => {
    if (inputDelayIsActive.value == true) return;
    console.log('hi c:');



    startInputDelay();
  }

  window.addEventListener('wheel', listenForInitialScrollorClick);
  window.addEventListener('click', listenForInitialScrollorClick);
});


const startInputDelay = () => {
  inputDelayIsActive.value = true;
  console.log('Input delay started');
  setTimeout(() => {
    inputDelayIsActive.value = false;
    console.log('Input delay ended');
  }, inputDelayLengthMs);
}
</script>

<template>
  <div id="main-wrapper">
    <div id="nav">
      <!-- This empty div becomes occupied visually when namecard "moves" -->
      <div id="nav-placeholder" :class="{ 'active': userHasScrolled }"></div>
    </div>

    <div id="side-by-side-main" :class="{ 'align-center-initial': !namecardHasMoved }">
      <div id="left-section-main" :class="{ 'full-width': !namecardHasMoved }">
        <!-- This h1 stays in DOM, but shifts position+style when userHasScrolled -->
        <h1 id="namecard" :class="{ 'shrink-header': userHasScrolled }">
          Cody
          <img id="namecard-img" src="../../assets/CodyPortfolioAnim.gif" />
          <br />
          Reeves
        </h1>
        <span id="prompt-text" class="primary-font light italic" :class="{ 'fade-out': userHasScrolled }">Scroll or
          click
          to learn
          more...</span>

        <div id="lower-section" :class="{ 'expand': userHasScrolled, 'scroll-into-view': namecardHasMoved }">
          <div id="rotating-title-container">
            <div id="title-top-divider"></div>
            <h2 id="rotating-title">Full Stack Developer</h2>
          </div>
          <div id="rotating-text-container">
            <div id="title-side-divider"></div>
            <p id="rotating-text">
              Some text about the current title that expands on it, and sells my skills a little bit.
            </p>
          </div>
        </div>
      </div>

      <div id="right-section-main" :class="{ 'scroll-into-view': namecardHasMoved }">
        <h1 style="font-size: 123px;">Some<br /> Image<br /> Here</h1>
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

:deep(#nav-namecard-container) {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

#nav {
  display: flex;
  height: 80px;
  align-items: center;
  padding: 0 20px;
  position: relative;
  border-bottom: 1px solid #ddd;
}

:deep(#prompt-text) {
  transition: color 3s ease-out;
  position: absolute;
  color: #c4b9b9;
  top: 72%;
  left: 50%;
  font-size: 18px;
  animation: infinite 3s pulse alternate;
}

@keyframes pulse {
  0% {
    color: #c4b9b9;
  }

  50% {
    color: #847d7d;
  }
}

.fade-out {
  color: rgb(0, 0, 0, 0) !important;
}

/* Empty placeholder in nav that can "catch" the namecard visually */
#nav-placeholder {
  width: 0;
  height: 0;
  transition: all 0.5s ease;
}

#nav-placeholder.active {
  width: auto;
  height: auto;
}

#side-by-side-main {
  display: flex;
}

@media screen and (max-width: 920px) {
  #side-by-side-main {
    flex-direction: column;
    align-items: center;
  }
}

#side-by-side-main.align-center-initial {
  justify-content: center;
  width: 100vw;
  overflow: hidden;
}

#namecard {
  font-size: 124px;
  font-family: "Roboto Serif", serif;
  font-style: italic;
  text-transform: uppercase;
  font-weight: 100;
  width: 100%;


  /* transition props for smooth anim */
  transition: position 1s ease;

  /* positioning for transition */
  position: relative;
  top: 0;
  left: 0;
  transform: none;
}

:deep(#nav-namecard-container>#namecard) {
  font-size: 32px;
}

:deep(#nav-namecard-container>#nav-img-container>#namecard-img) {
  width: 75px;
  height: 75px;
}

/* when user scrolls, shrink + reposition */
#namecard.shrink-header {
  font-size: 52px;
  position: fixed;
  top: 10px;
  left: 20px;
  transform: scale(1);
  z-index: 1000;
}

#side-by-side-main {
  display: flex;
}

#namecard-img {
  width: 150px;
  height: 150px;
  transition: width 0.5s ease, height 0.5s ease;
}

#namecard.shrink-header #namecard-img {
  width: 50px;
  height: 50px;
}


#rotating-title {
  font-family: "Roboto Serif", serif;
  font-weight: 200;
}

#rotating-title-container {
  min-height: 120px;
}

#rotating-text-container {
  min-height: 120px;
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

#left-section-main {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  transition: all 0.5s ease-in;
}

#left-section-main.full-width {
  width: 100%;
  align-items: center;
}

#left-section-main.full-width>h1#namecard {
  width: 100%;
}

#right-section-main {
  display: flex;
  justify-content: center;
  border-left: 1px solid #c2c2c2;
  transition: position 0.5s ease;
  transform: translate(50vw, 0px);

}

#right-section-main.scroll-into-view {
  transform: translate(0, 0);
}

#lower-section {
  display: flex;
  gap: 22px;
  transition: all 0.3s ease-in;
  transform: translate(-100vw, 0);
}

#lower-section:not(.expand) {
  color: rgba(0, 0, 0, 0);
}

#lower-section.expand {
  height: 100%;
  align-items: flex-end;
}

#lower-section.expand.scroll-into-view {
  transform: translate(0px, 0px);
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
  min-height: 120px;
  width: 0px;
  border-right: 1px solid #d2d2d2;
}
</style>
onimation: infinite pulse alternate slide-in;
