<template>
  <body>
    <!-- GymmBuddy x GymmBoxx Logo -->
    <div id="logo">
      <img src="/logo.png" alt="" />
    </div>
    <!-- Slogan -->
    <div id="slogan">
      <div class="container">
        <div class="row">
          <div class="col" id="tagline">
            <h1 style="font-size: 5rem">Fitness Made Easy</h1>
            <h4>
              An all-in-one platform that caters to you and your fitness trainer
            </h4>
            <!-- Sign Up Button -->
            <router-link to="/signup">
              <button class="pill-button">SIGN-UP</button>
            </router-link>
            <!-- Sign In Button -->
            <router-link to="/signin">
              <button class="pill-button">SIGN-IN</button>
            </router-link>
          </div>
          <!-- Image -->
          <div class="col" id="women-exercising">
            <img src="/women-exercising.jpg" alt="" width="500" style="box-shadow: 0px 0px 10px rgb(0,0,0,0.5);"/>
          </div>
        </div>
      </div>
    </div>

    <!-- About -->
    <div id="about">
      <div class="container">
        <h2 class="about-gymmbuddy">ABOUT</h2>
        <h2 class="about-gymmbuddy" style="color: #ed1f24">GYMMBUDDY</h2>
        <h5
          style="
            line-height: 2em;
            margin-top: 30px;
            margin: 0px 150px;
            font-size: 1.4rem;
          "
        >
          GYMMBUDDY is an exclusive web application that aids GYMMBOXX's clients
          in their fitness planning and enhances the client-trainer
          relationship. Our one-stop platform offers a range of features,
          including progress tracking and building custom workout routines. You
          can also book paid training sessions with your preferred trainer,
          making your fitness journey more personalized. Our aim is to provide a
          holistic approach to fitness by offering multiple features that are
          entirely free to use. With GYMMBUDDY, you can achieve your fitness
          goals with ease and convenience, making your fitness journey a more
          enjoyable experience. Sign up for GYMMBUDDY today and start your
          journey towards a healthier you!
        </h5>
      </div>
    </div>

    <!-- Reasons for using GYMMBUDDY-->
    <div id="reasons">
      <div class="container">
        <h2 class="why-gymmbuddy">WHY</h2>
        <h2 class="why-gymmbuddy" style="color: #ed1f24; margin-bottom: 30px">
          GYMMBUDDY
        </h2>
        <div class="row">
          <div class="col">
            <img src="/checklist.png" alt="" height="200px" width="250px" />
            <h4>TRACKING</h4>
          </div>
          <div class="col">
            <img src="/dumbbell.png" alt="" height="200px" width="250px" />
            <h4>PERSONALISED TRAINING</h4>
          </div>
          <div class="col">
            <img src="/thumb.png" alt="" height="200px" width="250px" />
            <h4>SIMPLE TO USE</h4>
          </div>
        </div>
      </div>
    </div>
  </body>
</template>

<script>
export default {
  name: "LandingPage",
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Hanken+Grotesk&family=Teko:wght@500;600&display=swap");

body {
  background-color: black;
  margin: 0px;
  padding: 0px;
  font-family: "Teko", sans-serif;
}

#women-exercising {
  margin: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}

#tagline {
  margin: 100px;
  box-sizing: border-box;
}

#logo {
  background-color: black;
  display: flex;
  align-items: center;
  justify-content: center;
}

#slogan {
  background-color: grey;
  color: white;
  margin-bottom: 50px;
}

#about {
  background-image: url("@/assets/images/profile_bg.jpg");
  background-size: contain;
  color: white;
  margin-bottom: 50px;
  padding: 50px;
  text-align: center;
  line-height: 5px;
}

#reasons {
  text-align: center;
  color: white;
  padding: 10px;
}
.btn {
  background-color: rgb(237, 31, 36);
  margin: 4px;
}

.pill-button:hover {
  animation-name: pill-button-highlight;
  animation-duration: 0.15s;
  animation-fill-mode: forwards;
  box-sizing: border-box;
}

@keyframes pill-button-highlight {
  from {
    border: 0px white solid;
  }
  to {
    border: 2px white solid;
  }
}
.pill-button {
  width: 120px;
  height: 50px;
  border-radius: 25px; /* half of height */
  background-color: rgb(237, 31, 36);
  border: none;
  outline: none;
  cursor: pointer;
  margin: 5px;
  margin-top: 30px;
  font-size: 1.5rem;
  text-align: center;
  box-sizing: border-box;
  color: white;
}

.about-gymmbuddy,
.why-gymmbuddy {
  display: inline-block;
  padding: 0px 5px;
  margin-bottom: 30px;
}
</style>
