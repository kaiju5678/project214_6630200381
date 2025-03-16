<template>
  <section
    id="aboutme"
    class="min-vh-100 d-flex align-items-center text-center"
  >
    <!-- Profile -->
    <div class="container">
      <!-- ข้อความข้างบน -->
      <div class="row">
        <div
          class="col-12 text-center"
          data-aos="fade-down"
          data-aos-delay="50"
        >
          <div class="section-title">
            <h1 class="display-4 fw-semibold">About Me</h1>
            <div class="line"></div>
            <p>This page is about My Profile</p>
          </div>
        </div>
      </div>

      <!-- แบ่ง 2 ฝั่ง -->
      <div class="row align-items-center">
        <!-- ฝั่งรูป -->
        <div class="col-lg-6 text-center">
          <div
            id="carouselExampleControls"
            class="carousel slide"
            data-bs-ride="carousel"
          >
            <div class="carousel-inner">
              <div class="carousel-item active">
                <img
                  src="../../images/img002.jpg"
                  class="d-block w-100 rounded-3"
                  alt=""
                />
              </div>
              <div class="carousel-item">
                <img
                  src="../../images/img003.jpg"
                  class="d-block w-100 rounded-3"
                  alt="..."
                />
              </div>
              <div class="carousel-item">
                <img
                  src="../../images/img004.jpg"
                  class="d-block w-100 rounded-3"
                  alt="..."
                />
              </div>
            </div>
            <button
              class="carousel-control-prev"
              type="button"
              data-bs-target="#carouselExampleControls"
              data-bs-slide="prev"
            >
              <span
                class="carousel-control-prev-icon"
                aria-hidden="true"
              ></span>
              <span class="visually-hidden">Previous</span>
            </button>
            <button
              class="carousel-control-next"
              type="button"
              data-bs-target="#carouselExampleControls"
              data-bs-slide="next"
            >
              <span
                class="carousel-control-next-icon"
                aria-hidden="true"
              ></span>
              <span class="visually-hidden">Next</span>
            </button>
          </div>
        </div>

        <!-- ฝั่ง About Me -->
        <div
          class="col-lg-6 d-flex flex-column justify-content-center align-items-end h-100 text-end"
          data-aos="fade-down"
          data-aos-delay="150"
        >
          <h1>Detail</h1>
          <p class="mt-3 mb-1">
            My name is
            <span class="fw-bold"
              >{{ name }} {{ lastname }} {{ id }} {{ sid }}</span
            >
          </p>
          <p class="mb-1">
            Study in <span class="fw-bold">{{ faculty }}</span> at
          </p>
          <p class="mb-1 fw-bold">{{ study }}</p>
          <div class="d-flex pt-4 mb-3">
            <div class="iconbox me-4">
              <i class="ri-mail-send-fill"></i>
            </div>
            <div>
              <h5>Education Detail</h5>
              <p>
                Graduated Kindergarten and Elementary School from
                <span class="fw-bold">{{ eleschool }}</span>
              </p>
              <p>
                Graduated Junior High School and High School from
                <span class="fw-bold">{{ highschool }}</span>
              </p>
            </div>
          </div>
          <button
            type="button"
            class="btn btn-warning"
            data-bs-toggle="modal"
            data-bs-target="#editModal"
          >
            Edit Data
          </button>
        </div>
      </div>
    </div>

    <!-- Modal สำหรับแก้ไขข้อมูล -->
    <div
      class="modal fade"
      id="editModal"
      tabindex="-1"
      aria-labelledby="editModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="editModalLabel">Edit Profile</h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <form @submit.prevent="saveChanges">
              <div class="mb-3">
                <label class="form-label">First Name</label>
                <input
                  type="text"
                  v-model="editData.name"
                  class="form-control"
                />
              </div>
              <div class="mb-3">
                <label class="form-label">Last Name</label>
                <input
                  type="text"
                  v-model="editData.lastname"
                  class="form-control"
                />
              </div>
              <div class="mb-3">
                <label class="form-label">Student ID</label>
                <input type="text" v-model="editData.id" class="form-control" />
              </div>
              <div class="mb-3">
                <label class="form-label">MajorID</label>
                <input
                  type="text"
                  v-model="editData.sid"
                  class="form-control"
                />
              </div>
              <div class="mb-3">
                <label class="form-label">Faculty</label>
                <input
                  type="text"
                  v-model="editData.faculty"
                  class="form-control"
                />
              </div>
              <div class="mb-3">
                <label class="form-label">Study At</label>
                <input
                  type="text"
                  v-model="editData.study"
                  class="form-control"
                />
              </div>
              <div class="mb-3">
                <label class="form-label">Elementary School</label>
                <input
                  type="text"
                  v-model="editData.eleschool"
                  class="form-control"
                />
              </div>
              <div class="mb-3">
                <label class="form-label">High School</label>
                <input
                  type="text"
                  v-model="editData.highschool"
                  class="form-control"
                />
              </div>
              <button type="submit" class="btn btn-primary">
                Save Changes
              </button>
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
      editData: {}, // ใช้เก็บข้อมูลที่กำลังแก้ไข
    };
  },
  methods: {
    openEditModal() {
      // คัดลอกค่าจากตัวแปรหลักไปยัง editData
      this.editData = { ...this.$data };
    },
    saveChanges() {
      // อัปเดตค่าหลักจาก editData
      Object.assign(this.$data, this.editData);
      // ปิด Modal
      let modal = document.getElementById("editModal");
      let modalInstance = bootstrap.Modal.getInstance(modal);
      modalInstance.hide();
    },
  },
};
</script>

<style>
.carousel-inner {
  width: 60%; /* กำหนดความกว้าง */
  margin: 0 auto; /* จัดกลาง */
}
.carousel-control-prev{
  width: 50%; /* กำหนดความกว้าง */
  margin: 0 auto; /* จัดกลาง */
}
.carousel-control-next{
  width: 50%; /* กำหนดความกว้าง */
  margin: 0 auto; /* จัดกลาง */
}


</style>
