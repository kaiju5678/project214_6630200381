<template>
  <section id="contact">
    <footer class="bg-dark text-white pt-5 pb-4 border-top border-secondary">
      <div class="container">
        <div class="row gy-5">
          <div class="col-lg-4 col-md-6">
            <h5 class="text-white fw-bold">Portfolio Project</h5>
            <div class="line mb-4"></div>
            <p class="text-white-50">
              This is a frontend development project for the subject 
              Practicum in Software Development (01418214).
            </p>
            <div class="social-icons mt-4">
              <a href="https://github.com/kaiju5678" target="_blank" title="GitHub">
                <i class="fa-brands fa-github"></i>
              </a>
              <a href="https://www.instagram.com/johan.kub_/" target="_blank" title="Instagram">
                <i class="fa-brands fa-instagram"></i>
              </a>
              <a href="https://www.facebook.com/johan.piyabordin/" target="_blank" title="Facebook">
                <i class="fa-brands fa-facebook-f"></i>
              </a>
              <a href="https://www.youtube.com/@Johan_Piyabordin" target="_blank" title="YouTube">
                <i class="fa-brands fa-youtube"></i>
              </a>
            </div>
          </div>

          <div class="col-lg-4 col-md-6">
            <h5 class="text-white fw-bold">Quick Links</h5>
            <div class="line mb-4"></div>
            <ul class="list-unstyled text-white-50">
              <li class="mb-2"><a href="#home" class="text-decoration-none text-reset hover-white">Home</a></li>
              <li class="mb-2"><a href="#aboutme" class="text-decoration-none text-reset hover-white">About Me</a></li>
              <li class="mb-2"><a href="#transcript" class="text-decoration-none text-reset hover-white">Transcript</a></li>
            </ul>
          </div>

          <div class="col-lg-4 col-md-12">
            <h5 class="text-white fw-bold">Contact Info</h5>
            <div class="line mb-4"></div>
            <ul class="list-unstyled text-white-50">
              <li class="mb-3 d-flex align-items-center">
                <i class="fa-solid fa-building-columns me-3 text-primary"></i>
                Dormitory Kasetsart University, Sriracha Campus
              </li>
              <li class="mb-3 d-flex align-items-center">
                <i class="fa-solid fa-globe me-3 text-primary"></i>
                <a href="https://dorms.src.ku.ac.th/" target="_blank" class="text-reset text-decoration-none hover-white">dorms.src.ku.ac.th</a>
              </li>
            </ul>
          </div>
        </div>
        
        <div class="row mt-5 pt-4 border-top border-secondary text-center">
            <div class="col-12">
                <p class="mb-0 text-white-50 small">&copy; 2025 Piyabordin. All Rights Reserved.</p>
            </div>
        </div>
      </div>
    </footer>
  </section>
</template>

<script>
export default {
  name: "Footers",
};
</script>

<style scoped>
.line {
  width: 40px;
  height: 3px;
  background-color: #4e57d4;
}

.social-icons a {
  width: 40px;
  height: 40px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  color: white;
  margin-right: 10px;
  text-decoration: none;
  transition: all 0.3s ease;
}

.social-icons a:hover {
  background-color: #4e57d4;
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(78, 87, 212, 0.4);
}

.hover-white:hover {
    color: white !important;
}
</style>