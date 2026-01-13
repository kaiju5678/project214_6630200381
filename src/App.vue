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

          <li class="nav-item ms-lg-3 mt-2 mt-lg-0">
            <button class="btn btn-theme-toggle" @click="toggleTheme" title="Switch Theme">
              <i class="fa-solid" :class="theme === 'dark' ? 'fa-sun' : 'fa-moon'"></i>
            </button>
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
    },
    toggleTheme() {
      // สลับค่า
      this.theme = this.theme === 'dark' ? 'light' : 'dark';
      // ตั้งค่า attribute ให้กับ html tag เพื่อให้ CSS จับค่าได้
      document.documentElement.setAttribute('data-theme', this.theme);
      // บันทึกลงเครื่อง (รีเฟรชเว็บแล้วธีมไม่หาย)
      localStorage.setItem('theme', this.theme);
    }
  },
  mounted() {
    // โหลดธีมเดิมที่เคยบันทึกไว้
    const savedTheme = localStorage.getItem('theme') || 'dark';
    this.theme = savedTheme;
    document.documentElement.setAttribute('data-theme', savedTheme);
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');

/* --- THEME CONFIGURATION --- */
:root {
  /* Dark Theme (ค่าเริ่มต้น) */
  --bg-color: #0f0f12;
  --section-bg-1: #1a1a1a; /* สีพื้นหลัง About Me เดิม */
  --section-bg-2: #121212; /* สีพื้นหลัง Transcript เดิม */
  --text-main: #e0e0e0;
  --text-muted: rgba(255, 255, 255, 0.5);
  --glass-nav: rgba(15, 15, 18, 0.8);
  --card-bg: rgba(40, 40, 40, 0.6);
  --border-color: rgba(255, 255, 255, 0.1);
  --btn-toggle-bg: rgba(255, 255, 255, 0.1);
  --shadow-card: 0 10px 30px rgba(0,0,0,0.5);
}

[data-theme="light"] {
  /* Light Theme (ปรับใหม่ให้สวยละมุน) */
  --bg-color: #f3f4f6;           /* พื้นหลังหลักสีเทาอ่อนมาก */
  --section-bg-1: #ffffff;       /* พื้นหลัง About Me สีขาว */
  --section-bg-2: #f8f9fa;       /* พื้นหลัง Transcript สีเทาจางๆ */
  --text-main: #2c3e50;          /* ตัวหนังสือสีน้ำเงินเข้มเกือบดำ (อ่านง่าย) */
  --text-muted: #64748b;         /* สีเทากลาง */
  --glass-nav: rgba(255, 255, 255, 0.8);
  --card-bg: #ffffff;            /* การ์ดสีขาว */
  --border-color: #e2e8f0;       /* เส้นขอบสีเทาอ่อน */
  --btn-toggle-bg: rgba(0, 0, 0, 0.05);
  --shadow-card: 0 10px 40px rgba(0,0,0,0.08); /* เงาฟุ้งๆ นุ่มๆ */
}

/* --- GLOBAL STYLES --- */
body {
  font-family: 'Poppins', sans-serif;
  background-color: var(--bg-color);
  color: var(--text-main);
  overflow-x: hidden;
  transition: background-color 0.4s ease, color 0.4s ease;
}

/* บังคับเปลี่ยนสีตามตัวแปร */
section {
  transition: background-color 0.4s ease;
}

/* Navbar */
.glass-nav {
  background: var(--glass-nav) !important;
  border-bottom: 1px solid var(--border-color) !important;
  backdrop-filter: blur(12px);
}

[data-theme="light"] .navbar-brand {
  background: linear-gradient(45deg, #2c3e50, #4e57d4) !important;
  -webkit-background-clip: text !important;
  -webkit-text-fill-color: transparent !important;
}

[data-theme="light"] .nav-link {
  color: #4b5563 !important;
}
[data-theme="light"] .nav-link:hover {
  color: #4e57d4 !important;
}

/* Card Overrides */
[data-theme="light"] .bg-dark, 
[data-theme="light"] .glass-card {
  background-color: var(--card-bg) !important;
  color: var(--text-main) !important;
  border: 1px solid var(--border-color) !important;
  box-shadow: var(--shadow-card) !important;
}

/* Text Overrides */
[data-theme="light"] .text-white { color: var(--text-main) !important; }
[data-theme="light"] .text-white-50 { color: var(--text-muted) !important; }

/* Table Overrides (แก้ Transcript) */
[data-theme="light"] .table-dark {
  background-color: transparent !important;
  color: var(--text-main) !important;
  --bs-table-bg: transparent !important;
  --bs-table-color: var(--text-main) !important;
  border-color: var(--border-color) !important;
}
[data-theme="light"] .table-dark th {
  background-color: #e2e8f0 !important; /* หัวตารางสีเทาอ่อน */
  color: #2c3e50 !important;
  border-bottom: 2px solid #cbd5e1 !important;
}
[data-theme="light"] .table-dark td {
  border-color: #e2e8f0 !important;
}

/* Footer Overrides */
[data-theme="light"] footer {
  background-color: #ffffff !important;
  border-top: 1px solid var(--border-color) !important;
}

/* เปลี่ยนสีวงกลมและไอคอนเมื่อเป็น Light Theme */
[data-theme="light"] .social-icons a {
  background-color: rgba(0, 0, 0, 0.05) !important; /* พื้นหลังวงกลมสีเทาอ่อน */
  color: #4e57d4 !important; /* ตัวไอคอนสีม่วง (Brand Color) */
  border: 1px solid rgba(0, 0, 0, 0.1); /* เพิ่มขอบบางๆ ให้เห็นชัดขึ้น */
}

/* ตอนเอาเมาส์ไปชี้ (Hover) */
[data-theme="light"] .social-icons a:hover {
  background-color: #4e57d4 !important; /* พื้นหลังเป็นสีม่วง */
  color: #ffffff !important; /* ไอคอนกลับเป็นสีขาว */
  border-color: #4e57d4 !important;
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(78, 87, 212, 0.3) !important;
}
/* --- FOOTER TEXT HOVER FIX --- */

/* ใน Light Mode: เมื่อเอาเมาส์ชี้ข้อความใน Footer ให้เปลี่ยนเป็นสีม่วง */
[data-theme="light"] .hover-white:hover {
  color: #4e57d4 !important; /* สี Brand (ม่วง) */
  font-weight: 600;           /* ตัวหนาขึ้นนิดนึง */
}

/* (แถม) ใน Light Mode: ลิงก์เบอร์โทรและอีเมล ก็ให้เปลี่ยนเป็นสีม่วงเหมือนกัน */
[data-theme="light"] footer a:hover {
  color: #4e57d4 !important;
}

/* --- MODAL CLOSE BUTTON FIX --- */

/* เมื่ออยู่ใน Light Mode ให้ปุ่มกากบาท (ที่เคยเป็นสีขาว) กลับมาเป็นสีดำ */
[data-theme="light"] .btn-close-white {
  filter: none !important; /* ยกเลิก Filter สีขาว */
  opacity: 0.5;            /* ปรับให้จางลงนิดนึงแบบมาตรฐาน */
}

/* เมื่อเอาเมาส์ชี้ใน Light Mode */
[data-theme="light"] .btn-close-white:hover {
  opacity: 1;              /* เข้มขึ้นเมื่อ Hover */
}

/* --- FORM INPUT PLACEHOLDER FIX --- */

/* Dark Mode: บังคับให้ตัวหนังสือตัวอย่าง (Placeholder) เป็นสีขาวจางๆ */
.form-control::placeholder {
  color: rgba(255, 255, 255, 0.5) !important;
  opacity: 1; /* จำเป็นสำหรับ Firefox */
}

/* Light Mode: บังคับให้กลับมาเป็นสีเทาเข้ม (เพื่อให้เห็นบนพื้นขาว) */
[data-theme="light"] .form-control::placeholder {
  color: rgba(0, 0, 0, 0.4) !important;
}

/* --- CUSTOM CAROUSEL BUTTONS --- */

/* ปรับพื้นที่กดให้เล็กลงหน่อย จะได้ไม่บังรูป */
.carousel-control-prev, .carousel-control-next {
  width: 15% !important;
  opacity: 1 !important; /* บังคับให้ชัดตลอดเวลา */
}

/* ดีไซน์ปุ่ม (วงกลม) - Dark Mode (Default) */
.carousel-btn-custom {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  
  /* Glass Effect (กระจกดำ) */
  background: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: white;
  
  /* จัดไอคอนให้อยู่ตรงกลาง */
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  
  transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275); /* เด้งดึ๋งๆ */
  box-shadow: 0 5px 15px rgba(0,0,0,0.3);
}

/* Hover Effect: ขยาย + เปลี่ยนสี */
.carousel-control-prev:hover .carousel-btn-custom,
.carousel-control-next:hover .carousel-btn-custom {
  background: #4e57d4; /* สีม่วง */
  border-color: #4e57d4;
  transform: scale(1.15); /* ขยายใหญ่ขึ้น */
  box-shadow: 0 0 20px rgba(78, 87, 212, 0.6); /* เรืองแสง */
}

/* --- LIGHT THEME OVERRIDE --- */
/* ดีไซน์ปุ่ม - Light Mode (กระจกขาว) */
[data-theme="light"] .carousel-btn-custom {
  background: rgba(255, 255, 255, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.1);
  color: #333; /* ไอคอนสีดำ */
}

/* Hover ใน Light Mode */
[data-theme="light"] .carousel-control-prev:hover .carousel-btn-custom,
[data-theme="light"] .carousel-control-next:hover .carousel-btn-custom {
  background: #4e57d4; /* กลับเป็นสีม่วงเมื่อชี้ */
  color: white;
  border-color: #4e57d4;
}

/* --- HOME TEXT FIX (LIGHT THEME) --- */

/* 1. บังคับให้หัวข้อ "Welcome to Project" ใน Light Mode กลับมาเป็นสีขาว */
[data-theme="light"] #home h1,
[data-theme="light"] #home .display-2 {
  color: #ffffff !important; 
  /* เปลี่ยน Glow จากสีม่วง เป็นสีขาวฟุ้งๆ ผสมฟ้า ให้ดูพรีเมียมแบบ Theme สว่าง */
  text-shadow: 0 0 20px rgba(255, 255, 255, 0.8), 0 0 40px rgba(78, 87, 212, 0.5) !important;
  
  /* (ลูกเล่นเสริม) ทำให้ตัวหนังสือดูเหมือนแก้ว/คริสตัล */
  background: linear-gradient(180deg, #ffffff 0%, #dbeafe 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

/* 2. บังคับให้ชื่อ "Piyabordin..." ใน Light Mode เป็นสีขาวชัดเจน */
/* 2. ส่วนชื่อ Piyabordin (แก้ใหม่! ให้ใช้สไตล์เดียวกับ Welcome) */
[data-theme="light"] #home h5,
[data-theme="light"] #home .text-white-50 {
  /* ใช้เทคนิคเดียวกับข้างบนเป๊ะๆ */
  background: linear-gradient(180deg, #ffffff 0%, #dbeafe 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  
  /* ลดความฟุ้งของเงาลงนิดหน่อยเพราะตัวหนังสือเล็กกว่า (จะได้ไม่อ่านยาก) */
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.8), 0 0 20px rgba(78, 87, 212, 0.5) !important;
  
  /* เพิ่มความหนาหน่อย เพราะพอมันใสแล้วจะดูบางลง */
  font-weight: 700 !important;
  letter-spacing: 1.5px;
  opacity: 1 !important;
}

/* --- FIX FONT CONSISTENCY (PIYABORDIN) --- */

/* กำหนดค่ากลางให้ชื่อ Piyabordin (ใช้ทั้ง Dark และ Light) */
#home h5,
#home .text-white-50 {
  font-weight: 700 !important;  /* บังคับตัวหนาเท่ากันเสมอ */
  letter-spacing: 1.5px;        /* ระยะห่างเท่ากันเสมอ */
  transition: all 0.4s ease;    /* เวลาเปลี่ยนสีให้สมูท */
}

/* (Dark Theme) ปรับสีให้ชัดขึ้นนิดนึงเพื่อให้แมทช์กับความหนาใหม่ */
#home h5 {
  color: rgba(255, 255, 255, 0.9);
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
}

/* Button Toggle */
.btn-theme-toggle {
  background-color: var(--btn-toggle-bg);
  color: var(--text-main);
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: 1px solid var(--border-color);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
}

/* --- เพิ่มส่วนนี้กลับเข้าไปครับ --- */

.nav-link {
  position: relative; /* สำคัญ! ใช้สำหรับยึดตำแหน่งเส้น */
  margin: 0 10px;
  font-weight: 500;
}

.nav-link::after {
  content: "";
  position: absolute;
  width: 0;
  height: 2px;
  bottom: 0;          /* ตำแหน่งเส้น (ชิดขอบล่าง) */
  left: 50%;
  background-color: #4e57d4; /* สีของเส้น (สีม่วง) */
  transition: all 0.3s ease-in-out;
  transform: translateX(-50%); /* จัดกึ่งกลาง */
  box-shadow: 0 0 10px #4e57d4; /* เงาเรืองแสง */
}

/* เมื่อเอาเมาส์ชี้ ให้ขยายความกว้างเส้นเป็น 100% */
.nav-link:hover::after {
  width: 100%;
}

/* ... CSS อื่นๆ (Video Background, Shapes) คงไว้เหมือนเดิม ... */
/* --- VIDEO BACKGROUND STYLE --- */
#home {
  position: relative;
  overflow: hidden;
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
  transition: transform 0.1s ease-out;
}
.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6); /* Overlay สีดำเสมอเพื่อให้ Video พื้นหลังอ่านง่าย */
  z-index: 1;
}
.z-2 { z-index: 2; }

/* Modern Button Keep */
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
.btn-modern .label { margin-right: 10px; transition: transform 0.4s ease; }
.btn-modern .icon { display: inline-flex; transform: translateX(0); transition: transform 0.4s ease; }
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
.btn-glass:hover .icon { transform: translateX(5px) rotate(15deg); }
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
.btn-neon:hover .shine { left: 100%; transition: 0.5s; }
.btn-neon:hover .label { transform: translateX(-5px); }
.btn-neon:hover .icon { transform: translateX(5px); }
</style>