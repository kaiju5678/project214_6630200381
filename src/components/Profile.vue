<template>
  <section id="aboutme">
    <div class="container h-100">
      <div class="d-flex flex-column justify-content-center h-100">
        
        <div class="row mb-4">
          <div class="col-12 text-center" data-aos="fade-down">
            <h1 class="display-4 fw-bold text-white">About Me</h1>
            <div class="line mx-auto"></div>
            <p class="text-secondary mt-2">Get to know me better</p>
          </div>
        </div>

        <div class="row align-items-center g-5">
          <div class="col-lg-6" data-aos="fade-right">
            <div
              id="profileCarousel"
              class="carousel slide shadow-lg rounded-4 overflow-hidden"
              data-bs-ride="carousel"
            >
              <div class="carousel-inner">
                <div class="carousel-item active">
                  <img
                    src="../../images/img001.jpg"
                    class="d-block w-100 object-fit-cover"
                    style="height: 450px;" 
                    alt="Profile 1"
                  />
                  </div>
                <div class="carousel-item">
                  <img
                    src="../../images/img002.jpg"
                    class="d-block w-100 object-fit-cover"
                    style="height: 450px;"
                    alt="Profile 2"
                  />
                </div>
                <div class="carousel-item">
                  <img
                    src="../../images/img003.jpg"
                    class="d-block w-100 object-fit-cover"
                    style="height: 450px;"
                    alt="Profile 3"
                  />
                </div>
                <div class="carousel-item">
                  <img
                    src="../../images/img004.jpg"
                    class="d-block w-100 object-fit-cover"
                    style="height: 450px;"
                    alt="Profile 3"
                  />
                </div>
              </div>
              <button
                class="carousel-control-prev"
                type="button"
                data-bs-target="#profileCarousel"
                data-bs-slide="prev"
              >
                <span class="carousel-control-prev-icon p-3 bg-dark rounded-circle bg-opacity-50" aria-hidden="true"></span>
              </button>
              <button
                class="carousel-control-next"
                type="button"
                data-bs-target="#profileCarousel"
                data-bs-slide="next"
              >
                <span class="carousel-control-next-icon p-3 bg-dark rounded-circle bg-opacity-50" aria-hidden="true"></span>
              </button>
            </div>
          </div>

          <div class="col-lg-6" data-aos="fade-left">
            <div class="card bg-dark text-white border-0 shadow-lg p-4 rounded-4 glass-card">
              <div class="card-body">
                <h2 class="card-title fw-bold mb-3 text-primary">Personal Details</h2>
                
                <div class="mb-3">
                  <p class="fs-5 mb-1">Hello, I am</p>
                  <h3 class="fw-bold">{{ name }} {{ lastname }}</h3>
                  <p class="text-white-50 small">ID: {{ id }} | Section: {{ sid }}</p>
                </div>

                <div class="mb-3">
                  <div class="d-flex align-items-start mb-2">
                    <div class="icon-box me-3">
                      <i class="fa-solid fa-graduation-cap fs-5"></i>
                    </div>
                    <div>
                      <h6 class="fw-bold mb-0">Current Education</h6>
                      <p class="mb-0 text-white-50 small">Faculty of {{ faculty }}</p>
                      <p class="mb-0 text-primary small">{{ study }}</p>
                    </div>
                  </div>
                  
                  <div class="d-flex align-items-start">
                    <div class="icon-box me-3">
                      <i class="fa-solid fa-school fs-5"></i>
                    </div>
                    <div>
                      <h6 class="fw-bold mb-0">Background</h6>
                      <p class="mb-0 text-white-50 small"><small>Elem:</small> {{ eleschool }}</p>
                      <p class="mb-0 text-white-50 small"><small>High:</small> {{ highschool }}</p>
                    </div>
                  </div>
                </div>

                <div class="text-end mt-3">
                  <button
                    type="button"
                    class="btn btn-outline-warning rounded-pill px-4 btn-sm"
                    data-bs-toggle="modal"
                    data-bs-target="#editModal"
                    @click="openEditModal"
                  >
                    <i class="fa-solid fa-pen-to-square me-2"></i>Edit Data
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div
      class="modal fade"
      id="editModal"
      tabindex="-1"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content bg-dark text-white border-secondary">
          <div class="modal-header border-secondary">
            <h5 class="modal-title">Edit Profile</h5>
            <button
              type="button"
              class="btn-close btn-close-white"
              data-bs-dismiss="modal"
            ></button>
          </div>
          <div class="modal-body">
            <form @submit.prevent="saveChanges">
              <div class="row g-3">
                <div class="col-md-6">
                  <label class="form-label text-secondary">First Name</label>
                  <input type="text" v-model="editData.name" class="form-control bg-dark border-secondary text-white" />
                </div>
                <div class="col-md-6">
                  <label class="form-label text-secondary">Last Name</label>
                  <input type="text" v-model="editData.lastname" class="form-control bg-dark border-secondary text-white" />
                </div>
                <div class="col-md-6">
                   <label class="form-label text-secondary">Student ID</label>
                   <input type="text" v-model="editData.id" class="form-control bg-dark border-secondary text-white" />
                </div>
                <div class="col-md-6">
                   <label class="form-label text-secondary">Section</label>
                   <input type="text" v-model="editData.sid" class="form-control bg-dark border-secondary text-white" />
                </div>
                 <div class="col-12">
                   <label class="form-label text-secondary">Faculty</label>
                   <input type="text" v-model="editData.faculty" class="form-control bg-dark border-secondary text-white" />
                </div>
                 <div class="col-12">
                   <label class="form-label text-secondary">University</label>
                   <input type="text" v-model="editData.study" class="form-control bg-dark border-secondary text-white" />
                </div>
                 <div class="col-12">
                   <label class="form-label text-secondary">Elementary School</label>
                   <input type="text" v-model="editData.eleschool" class="form-control bg-dark border-secondary text-white" />
                </div>
                 <div class="col-12">
                   <label class="form-label text-secondary">High School</label>
                   <input type="text" v-model="editData.highschool" class="form-control bg-dark border-secondary text-white" />
                </div>
              </div>
              <div class="mt-4 d-grid">
                <button type="submit" class="btn btn-primary">Save Changes</button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "Profile",
  data() {
    return {
      name: "Piyabordin",
      lastname: "Pisitphanpong",
      id: 6630200381,
      sid: "S05",
      faculty: "Computer Science",
      study: "Kasetsart University Sriracha Campus",
      eleschool: "Somapa Pattana School",
      highschool: "Satriwitthaya 2 School",
      editData: {},
    };
  },
  methods: {
    openEditModal() {
      this.editData = { ...this.$data };
    },
    saveChanges() {
      Object.assign(this.$data, this.editData);
      let modalElement = document.getElementById("editModal");
      let modalInstance = bootstrap.Modal.getInstance(modalElement);
      modalInstance.hide();
    },
  },
};
</script>

<style scoped>
#aboutme {
  background-color: #1a1a1a;
  /* Key Changes: Fix Height and Padding */
  height: 100vh; /* บังคับความสูงเท่าจอภาพเป๊ะๆ */
  padding-top: 80px; /* เว้นที่ด้านบนให้ Navbar (ปรับค่านี้ถ้า Navbar สูงกว่า 80px) */
  box-sizing: border-box; /* รวม Padding เข้าไปในความสูง */
  overflow: hidden; /* ป้องกันส่วนเกินล้นออกมา */
}

/* ปรับแต่งเล็กน้อยเพื่อให้ Fit กับจอ */
.line {
  width: 60px;
  height: 4px;
  background-color: #4e57d4;
  margin-top: 10px;
}

.glass-card {
  background: rgba(40, 40, 40, 0.6);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.icon-box {
  width: 45px;
  height: 45px;
  background-color: rgba(78, 87, 212, 0.2);
  color: #4e57d4;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>