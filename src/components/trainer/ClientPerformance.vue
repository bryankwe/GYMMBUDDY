<template>
  <div class="performance-page">
    <TrainerNavbar />
    <!-- Creating the specified client email performance page -->
    <TrainerPerformanceHeader
      :email="clientEmail"
      :profilePic="profilePicURL"
      @returnToHome="returnBackToTrainerHomePage()"
      @routeToRoutine="routeToRoutinePage()"
    />
    <div class="content-container">
      <AllCharts :email="clientEmail" />
      <PerformanceBottom class="bottom" :email="clientEmail" />
    </div>
  </div>
</template>

<script>
import AllCharts from "../client/AllCharts.vue";
import PerformanceBottom from "../client/PerformanceBottom.vue";
import TrainerPerformanceHeader from "./TrainerPerformanceHeader.vue";
import TrainerNavbar from "./TrainerNavbar.vue";

export default {
  name: "ClientPerformancePage",
  props: ["clientEmail", "profilePicURL"],
  components: {
    AllCharts,
    PerformanceBottom,
    TrainerPerformanceHeader,
    TrainerNavbar,
  },
  methods: {
    // return back to the client selection menu when the method is run
    returnBackToTrainerHomePage() {
      this.$emit("returnToHome");
    },
    // goes to the routine page when the method is run
    routeToRoutinePage() {
      this.$emit("routeToRoutine");
    },
  },
  emits: ["returnToHome", "routeToRoutine"],
};
</script>
<style scoped>
.performance-page {
  background-color: black;
  overflow-y: hidden;
  min-width: 800px; /* Or else the PerformanceBottom component will overflow into the side margin */
  padding-bottom: 50px;
}

.content-container {
  background-color: #d9d9d9;
  margin: 0vw 10vw;
  border-radius: 25px;
  padding-bottom: 30px;
  margin-top: 22px;
}

body::-webkit-scrollbar {
  display: none;
}
</style>
