<template>
  <div class="progress-section-container">
    <div class="progress-header">
      <ComponentHeader :blackHeader="blackHeader" :redHeader="redHeader" />
    </div>
    <div class="progress-chart-container">
      <!-- Create the ProgressChart for Weight -->
      <ProgressChartNew
        chartName="Weight"
        :progressOutput="weightData.Progress"
        :goal="weightGoal"
        :chartSeries="weightArray"
      />
      <!-- Creates the ProgressChart for Muscle Mass -->
      <ProgressChartNew
        chartName="Muscle Mass"
        :progressOutput="muscleData.Progress"
        :goal="muscleGoal"
        :chartSeries="muscleArray"
      />
    </div>
  </div>
</template>

<script>
import { db, auth } from "../../firebase.js";
import { collection, getDocs, query, where } from "firebase/firestore";
import { useStore, mapGetters } from "vuex";

import ProgressChartNew from "./ProgressChartNew.vue";
import ComponentHeader from "./ComponentHeader.vue";
export default {
  name: "ProgressSection",
  data() {
    return {
      blackHeader: "Current",
      redHeader: "Progress",
      weightGoal: null,
      weightData: {
        Progress: null,
        Remaining: null,
      },
      weightArray: [],
      muscleGoal: null,
      muscleData: {
        Progress: null,
        Remaining: null,
      },
      muscleArray: [],
    };
  },
  props: {
    email: String,
  },
  computed: {
    ...mapGetters(["user"]),
  },
  components: {
    ProgressChartNew,
    ComponentHeader,
  },
  mounted() {
    const store = useStore();
    auth.onAuthStateChanged((user) => {
      store.dispatch("fetchUser", user);
    });
  },
  async created() {
    try {
      const clientRef = collection(db, "client");
      const q = query(clientRef, where("email", "==", this.email));
      const querySnapshot = await getDocs(q);

      querySnapshot.forEach((doc) => {
        // Retrieving the only data with the correct email
        let documentData = doc.data();

        // storing the latest information for weight and muscle mass
        let weightData = documentData.weight.slice(-1)[0];
        let muscleMassData = documentData.muscleMass.slice(-1)[0];

        // storing the goals
        let weightGoalValue = documentData.goals["weightGoal"];
        let muscleMassGoalValue = documentData.goals["muscleMassGoal"];

        // Declare the progress variable
        let weightProgress;

        if (weightData < weightGoalValue) {
          // if goal has not been hit
          // Compute the progress and save in number format
          weightProgress = Number(
            Number((weightData / weightGoalValue) * 100).toFixed()
          );
        } else {
          // if goal is hit or exceeded
          weightProgress = 100;
        }

        // Declare the progress variable
        let muscleMassProgress;

        if (muscleMassData < muscleMassGoalValue) {
          // Compute the progress
          muscleMassProgress = Number(
            Number((muscleMassData / muscleMassGoalValue) * 100).toFixed()
          );
        } else {
          // if goal is hit or exceeded
          // console.log("Entered else condition");
          muscleMassProgress = 100;
        }

        // Assign the values to data()
        this.weightGoal = `${weightGoalValue}kg`;
        // If currently no data ==> Can't have a progress!
        if (documentData.weight.length === 0) {
          this.weightData.Progress = 0;
        } else {
          this.weightData.Progress = weightProgress;
        }
        this.weightData.Remaining = 100 - this.weightData.Progress;
        this.weightArray.push(this.weightData.Progress);
        this.weightArray.push(this.weightData.Remaining);

        this.muscleGoal = `${muscleMassGoalValue}%`;
        // If currently no data ==> Can't have a progress!
        if (documentData.muscleMass.length === 0) {
          this.muscleData.Progress = 0;
        } else {
          this.muscleData.Progress = muscleMassProgress;
        }
        this.muscleData.Remaining = 100 - this.muscleData.Progress;
        this.muscleArray.push(this.muscleData.Progress);
        this.muscleArray.push(this.muscleData.Remaining);
      });
    } catch (error) {
      console.log(error);
      console.log("No email observed in database");
    }
  },
};
</script>

<style scoped>
.progress-section-container {
  /* background: rgba(0, 0, 0, 0.3);
  border-radius: 25px;
  display: inline-block;
  height: 34.5vh;
  box-sizing: border-box; */
  display: flex;
  flex-direction: column;
  /* height: 34.5vh; */
  width: 100%;
  box-sizing: border-box;
  padding: 15px;
}

.progress-chart-container {
  display: flex;
  justify-content: space-evenly;
}
</style>