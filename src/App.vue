<template>
  <div id="app">
    <img 
      src="@/assets/media/mifkada-logo.png"
      class="logo"
      alt="Logo"
    />
  
    <img
      src="@/assets/media/madortill.png"
      alt="mador-till"
      class="mador-till"
    />

    <button v-show ="page === 0" class = "aboutBtn" @click = "openAbout">i</button>
    <Transition>
          <div v-show ="showAbout && page===0" class="div-about">
          <h3 class = "list-text-about">מפתחת ראשית:</h3>
            <p class = "list-text-about">רב"ט דורון הרפז</p>
            <h3 class = "list-text-about">גרפיקה:</h3>
            <p class = "list-text-about">רב"ט דורון הרפז</p>
            <h3 class = "list-text-about">מומחית תוכן:</h3>
            <p class = "list-text-about">רב"ט אלה טייטלר</p>
            <h3 class = "list-text-about">רת"ח מו"פ:</h3>
            <p class = "list-text-about">רס"ל אביב אואנונו</p>
            <h3 class = "list-text-about">רמ"ד טי"ל:</h3>
            <p class = "list-text-about">רס"מ שלומי אוגרן</p>
            <h3 class = "list-text-about">גרסה:</h3>
            <p class = "list-text-about">יולי 2024</p>
        </div>
    </Transition>

    <openScreen v-if="page === 0"  @next-page="nextPage"></openScreen>
    <navbar v-if="showNav" :titleIndex="titleIndex" @chosen-title="chosenPage" :maxNavPos="maxNavPos"></navbar>
    <basic-principles v-if="page === 1" @next-page="nextPage"></basic-principles>
    <process v-if="page === 2" @next-page="nextPage"></process>
    <preparation v-if="page === 3" @next-page="nextPage"></preparation>
    <practice v-if="page === 4" @next-page="nextPage"></practice>
    <end-screen v-if="page === 5"></end-screen>


  </div>
</template>

<script>
import OpenScreen from "@/components/OpenScreen.vue";
import Navbar from '@/components/Navbar.vue';
import BasicPrinciples from '@/components/BasicPrinciples.vue';
import Process from '@/components/Process.vue';
import Preparation from '@/components/Preparation.vue';
import Practice from '@/components/Practice.vue';
import EndScreen from '@/components/EndScreen.vue';



export default {
  name: "app",
  components: {
    OpenScreen,
    Navbar,
    BasicPrinciples,
    Process,
    Preparation,
    Practice,
    EndScreen,

  },

  data() {
    return {
      page: 0,
      titleIndex: -1,
      showNav: true,
      showAbout: false,
      clickBtn: 0,
      maxNavPos: 0
    };
  },
  methods: {
    nextPage() {
      this.page++;
      this.titleIndex++;
      this.maxNavPos = Math.max(this.maxNavPos, this.titleIndex);
    },

    chosenPage(index) {
      this.titleIndex = index;
      this.page = this.titleIndex + 1;
      console.log(this.page);

      this.maxNavPos = Math.max(this.maxNavPos, index);
    },

    openAbout() {
          if (this.clickBtn % 2 === 0) {
                this.showAbout = true;
            } else {
                this.showAbout = false;
            }
            this.clickBtn++;
        },
  },
};
</script>

<style scoped>
@font-face {
  font-family: "Heebo";
  src: url("@/assets/fonts/heebo.regular.ttf");
}

@font-face {
  font-family: "Heebo-Bold";
  src: url("@/assets/fonts/heebo.black.ttf");
}

* {
  overflow: hidden;
  font-family: "Heebo";
  direction: rtl;
}

body {
  margin: 0;
  direction: rtl;
}

#app {
  width: 100vw;
  height: 100vh;
  position: relative;
  background-color: #ebdef8;

}

.logo {
  max-width: 100px;
  position: absolute;
  top: 2%;
  left: 1%;
  z-index: 3;
}

.mador-till {
  max-height: 10%;
  max-width: 90px;
  position: absolute;
  bottom: 1%;
  right: 1%;
  z-index: 3;
}

.aboutBtn {
  position: absolute;
  border: none;
  color: white;
  font-size: 1.6rem;
  transition: background-color 0.3s ease;
  background-color: #02ade1;
  border-radius: 150px;
  width: 2%;
  height: 4%;
  cursor: pointer;
  left: 2.5%;
  top: 15%;

}

.aboutBtn:hover{
  background-color: #038eb9;
}

.div-about {
  position: absolute;
  width: 12%;
  height: 50%;
  left: 8%;
  top: 10%;
  background: #fff;
  border-radius: 1rem;
  box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
  text-align: center;
}

.list-text-about {
  transition: background-color 0.5s ease;
  margin: 5%;
}

.list-text-about:hover {
  background-color: #dbdbdb;
}
</style>
