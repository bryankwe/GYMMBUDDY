<template>
  <div class="performance-page">
    <div>
      <Navbar />
    </div>
    <PerformanceHeader />
    <div class="content-container">
      <AllCharts :email="email" />
      <PerformanceBottom class="bottom" :email="email" />
    </div>
  </div>
</template>

<script>
import { mapGetters, useStore } from "vuex";
import {db, auth} from "../../firebase.js"
import AllCharts from "../client/AllCharts.vue";
import PerformanceBottom from "../client/PerformanceBottom.vue";
import PerformanceHeader from "../client/PerformanceHeader.vue";

export default {
  name: "PerformancePage",
  computed: {
    ...mapGetters(["user"]),
  },
  data() {
    return {
      email: "",
    };
  },
  mounted() {
    const store = useStore();
    auth.onAuthStateChanged((user) => {
      store.dispatch("fetchUser", user);
    }); // whenever page refreshes, the auth will have a short buffer from unknown to signed in / signed out
  },
  async created() {
    this.email = this.user.data.email; // setting and passing the prop down to allcharts
  },
  components: {
    AllCharts,
    PerformanceBottom,
    PerformanceHeader,
  },
};
</script>

<style scoped>
.performance-page {
  background-color: black;
  overflow-y: hidden;
  min-width: 800px; /* Or else the PerformanceBottom component will overflow into the side margin */
  min-height: 100vh;
  padding-bottom: 50px;
}

@media screen and (max-width: 800px) {
  .performance-page {
    padding-bottom: calc(50px + 50vh)
  }
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