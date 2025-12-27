<template>
  <nav class="navbar navbar-expand-lg fixed-top navbar-dark glass-nav">
    <div class="container">
      <a class="navbar-brand fw-bold" href="#">
        <i class="fa-solid fa-code me-2"></i>Portfolio
      </a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
        aria-controls="navbarNav">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item">
            <a class="nav-link" href="#home">Home</a>
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

  <section id="home" class="min-vh-100 d-flex align-items-center text-center" @mousemove="handleMouseMove">
    <div class="video-wrapper">
      <video autoplay loop muted playsinline class="bg-video" :style="videoStyle">
        <source src="@/assets/bg-video.mp4" type="video/mp4">
        Your browser does not support the video tag.
      </video>
    </div>

    <div class="overlay"></div>

    <div class="container position-relative z-2">
      <div class="row justify-content-center">
        <div class="col-lg-10">
          <h1 data-aos="fade-up" class="text-uppercase text-white fw-bold display-2 mb-3"
            style="letter-spacing: 2px; text-shadow: 0 0 20px rgba(78, 87, 212, 0.5);">
            Welcome to Project
          </h1>
          <h5 class="text-white-50 mt-3 mb-5" data-aos="fade-up" data-aos-delay="100">
            Piyabordin Pisitphanpong's Portfolio
          </h5>

          <div data-aos="fade-up" data-aos-delay="200" class="d-flex gap-3 justify-content-center">
            <a href="#aboutme" class="btn-modern btn-glass">
              <span class="label">View Profile</span>
              <span class="icon"><i class="fa-regular fa-user"></i></span>
            </a>

            <a href="#transcript" class="btn-modern btn-neon">
              <span class="label">View Transcript</span>
              <span class="icon"><i class="fa-solid fa-file-lines"></i></span>
              <div class="shine"></div>
            </a>
          </div>

        </div>
      </div>
    </div>
  </section>

  <Profile />

  <Transcript />

  <Footers />
</template>

<script>
import Profile from "./components/Profile.vue";
import Transcript from "./components/Transcript.vue";
import Footers from "./components/Footers.vue";

export default {
  name: "App",
  components: { Profile, Transcript, Footers },
  data() {
    return {
      mouseX: 0,
      mouseY: 0,
    };
  },
  computed: {
    videoStyle() {
      // คำนวณการขยับ (หารด้วย 30 เพื่อให้ขยับนุ่มๆ ไม่เวียนหัว)
      // ต้องมี scale(1.1) เพื่อขยายวิดีโอให้ใหญ่กว่าจอ เวลาขยับขอบจะได้ไม่หลุด
      const moveX = this.mouseX / -30;
      const moveY = this.mouseY / -30;
      return {
        transform: `scale(1.1) translate(${moveX}px, ${moveY}px)`
      };
    }
  },
  methods: {
    handleMouseMove(event) {
      this.mouseX = event.clientX - window.innerWidth / 2;
      this.mouseY = event.clientY - window.innerHeight / 2;
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');

/* Reset & Global */
body {
  font-family: 'Poppins', sans-serif;
  background-color: #0f0f12;
  color: #e0e0e0;
  overflow-x: hidden;
}

/* Navbar Style */
.glass-nav {
  background: rgba(15, 15, 18, 0.8);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  padding: 15px 0;
  transition: all 0.3s ease;
}

.navbar-brand {
  font-size: 1.5rem;
  letter-spacing: 1px;
  background: linear-gradient(45deg, #fff, #a5a5a5);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.nav-link {
  color: #b0b0b0 !important;
  margin: 0 10px;
  position: relative;
  font-weight: 500;
  transition: color 0.3s;
}

.nav-link::after {
  content: "";
  position: absolute;
  width: 0;
  height: 2px;
  bottom: -4px;
  left: 50%;
  background-color: #4e57d4;
  transition: all 0.3s ease-in-out;
  transform: translateX(-50%);
  box-shadow: 0 0 10px #4e57d4;
}

.nav-link:hover::after {
  width: 100%;
}

.nav-link:hover {
  color: #fff !important;
}

/* --- VIDEO BACKGROUND STYLE --- */
#home {
  position: relative;
  overflow: hidden;
  /* สำคัญมาก: ตัดส่วนเกินของวิดีโอทิ้ง */
}

.video-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  overflow: hidden;
}

.bg-video {
  width: 100%;
  height: 100%;
  object-fit: cover;
  /* ให้วิดีโอเต็มจอโดยไม่เสียสัดส่วน */
  /* transition: transform 0.1s ease-out; ใส่ตรงนี้เพื่อให้ลื่นไหล */
  transition: transform 0.1s ease-out;
}

/* Overlay: สีดำจางๆ ทับวิดีโอ */
.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  /* ปรับความเข้มตรงนี้ 0.6 = 60% */
  z-index: 1;
}

.z-2 {
  z-index: 2;
}

/* --- MODERN BUTTONS STYLE (KEEP) --- */
.btn-modern {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 15px 35px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  text-decoration: none;
  border-radius: 50px;
  overflow: hidden;
  transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
  z-index: 1;
}

.btn-modern .label {
  margin-right: 10px;
  transition: transform 0.4s ease;
}

.btn-modern .icon {
  display: inline-flex;
  transform: translateX(0);
  transition: transform 0.4s ease;
}

/* Glass Button */
.btn-glass {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: #e0e0e0;
  backdrop-filter: blur(10px);
}

.btn-glass:hover {
  background: rgba(255, 255, 255, 0.15);
  border-color: #fff;
  color: #fff;
  box-shadow: 0 0 20px rgba(255, 255, 255, 0.2);
  transform: translateY(-3px);
}

.btn-glass:hover .icon {
  transform: translateX(5px) rotate(15deg);
}

/* Neon Button */
.btn-neon {
  background: linear-gradient(135deg, #4e57d4, #8a2be2);
  border: none;
  color: white;
  box-shadow: 0 4px 15px rgba(78, 87, 212, 0.4);
}

.btn-neon .shine {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
  transition: 0.5s;
  z-index: -1;
  transform: skewX(-20deg);
}

.btn-neon:hover {
  color: white;
  box-shadow: 0 0 25px rgba(138, 43, 226, 0.6), 0 0 10px rgba(78, 87, 212, 0.8);
  transform: translateY(-3px) scale(1.02);
}

.btn-neon:hover .shine {
  left: 100%;
  transition: 0.5s;
}

.btn-neon:hover .label {
  transform: translateX(-5px);
}

.btn-neon:hover .icon {
  transform: translateX(5px);
}
</style>