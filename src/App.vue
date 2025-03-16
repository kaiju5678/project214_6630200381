<template>
  <!-- NavBar -->
  <nav class="navbar navbar-expand-lg sticky-top">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Portfolio</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item">
            <a class="nav-link" href="#">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#aboutme">About Me</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#transcript">Transcript</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#contact">Contact</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <!-- Welcome Page -->
  <section id="home" class="min-vh-100 d-flex align-items-center text-center">
    <div class="container position-relative">
      <div class="row">
        <div class="col-12">
          <h1
            data-aos="fade-left"
            class="text-uppercase text-white fw-semibold display-1"
          >
            Welcome to Project
          </h1>
          <h5 class="text-white mt-3 mb-4" data-aos="fade-right"></h5>
          <div data-aos="fade-up" data-aos-delay="50">
            <a href="#aboutme" class="btn btn-light me-2 fw-medium">Profile</a>
            <a href="#transcript" class="btn btn-light ms-2 fw-medium"
              >Transcript</a
            >
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Profile -->
  <div>
    <Profile/>
  </div>

  <!-- Transcript -->
  <div>
    <Transcript/>
  </div>

  <div>
    <Footers/>
  </div>

</template>

<script>
import Profile from "./components/Profile.vue";
import Transcript from "./components/Transcript.vue";
import Footers from "./components/Footers.vue";

export default {
  name: "App",
  components: { Profile, Transcript, Footers },
};
</script>
<style>
#home {
  position: relative;
  background-image: url("../images/img001.jpg");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}

#home::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5); /* ปรับค่าความมืดตามต้องการ */
}

.navbar-brand{
  color: whitesmoke;
}

.navbar {
  box-shadow: #212529;
  background-color: #727272;
}

.navbar-nav .nav-link {
  font-weight: 500;
  color: whitesmoke;
}

.nav-link {
  position: relative;
}
.nav-link:hover {
  color: black;
}

.nav-link::after {
  content: "";
  opacity: 0;
  transition: all 0.5s;
  height: 2px;
  width: 100%;
  background-color: black;
  position: absolute;
  bottom: 0;
  left: 0;
}

.nav-link:hover::after {
  opacity: 1;
}
</style>
