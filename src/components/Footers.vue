<template>
  <section id="contact">
    <footer class="bgfooter">
      <div class="footer-top">
        <div class="container">
          <div class="row gy-5">
            <div class="col-lg-3 col-sm-6">
              <h5 class="mb-0 text-white">Description</h5>
              <div class="line"></div>
              <p>
                This is a frontend develop Project in Subject Practicum in
                Software Development 01418214
              </p>
              <div class="social-icons">
                <a href="https://github.com/kaiju5678"
                  ><i class="fa-brands fa-github"></i
                ></a>
                <a href="https://www.instagram.com/johan.kub_/"
                  ><i class="fa-brands fa-instagram"></i
                ></a>
                <a href="https://www.facebook.com/johan.piyabordin/"
                  ><i class="fa-brands fa-facebook"></i
                ></a>
                <a href="https://www.youtube.com/@Johan_Piyabordin"
                  ><i class="fa-brands fa-youtube"></i
                ></a>
              </div>
            </div>
            <div class="col-lg-3 col-sm-6"></div>
            <div class="col-lg-3 col-sm-6"></div>
            <div class="col-lg-3 col-sm-6">
              <h5 class="mb-0 text-white">CONTACT</h5>
              <div class="line"></div>
              <ul>
                <li>Dormitory Kasetsart University</li>
                <li>Sriracha Campus</li>
                <li>dorms.src.ku.ac.th/</li>
              </ul>
            </div>
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

<style>
.bgfooter {
  background-color: #727272;
}
footer {
  padding-top: 120px;
}

.footer-top {
  padding-bottom: 40px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.footer-bottom {
  padding-top: 40px;
  padding-bottom: 40px;
}

footer li,
footer p,
footer a {
  color: rgba(255, 255, 255, 0.7);
}

footer ul {
  list-style: none;
  padding: 0;
}

footer .line {
  width: 40px;
  height: 4px;
  background-color: whitesmoke;
  margin-top: 12px;
  margin-bottom: 24px;
}

.social-icons a {
  width: 40px;
  height: 40px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 100px;
}

.social-icons a:hover {
  background-color: #4e57d4;
  color: white;
}
</style>
