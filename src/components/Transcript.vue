<template>
  <section
    id="transcript"
    class="min-vh-100 d-flex align-items-center text-center border-top"
  >
    <div class="container mt-5">
      <h2 class="text-center mb-4">รายการข้อมูล</h2>

      <table class="table table-striped table-bordered text-center">
        <thead class="table-dark">
          <tr>
            <th>ลำดับ</th>
            <th>Subject Name</th>
            <th>Subject ID</th>
            <th>Credit</th>
            <th>Grade</th>
            <th>Edit / Delete</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in items" :key="item.id || index">
            <td>{{ index + 1 }}</td>
            <td>{{ item.subjectname }}</td>
            <td>{{ item.subjectid }}</td>
            <td>{{ item.credit }}</td>
            <td>{{ item.grade }}</td>
            <td>
              <button
                class="btn btn-warning btn-sm me-2"
                @click="editRow(item)"
              >
                แก้ไข
              </button>
              <button class="btn btn-danger btn-sm" @click="deleteRow(item)">
                ลบ
              </button>
            </td>
          </tr>
        </tbody>
      </table>

      <div class="text-center">
        <button
          class="btn btn-primary"
          data-bs-toggle="modal"
          data-bs-target="#addModal"
          @click="resetForm"
        >
          เพิ่มข้อมูล
        </button>
      </div>

      <div class="modal fade" id="addModal" tabindex="-1" aria-hidden="true">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">
                {{ isEditing ? "แก้ไขข้อมูล" : "เพิ่มข้อมูล" }}
              </h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
              ></button>
            </div>
            <div class="modal-body">
              <form @submit.prevent="saveData">
                <div class="mb-3">
                  <label class="form-label">Subject Name</label>
                  <input
                    type="text"
                    v-model="formData.subjectname"
                    class="form-control"
                    required
                  />
                </div>
                <div class="mb-3">
                  <label class="form-label">Subject ID</label>
                  <input
                    type="text"
                    v-model="formData.subjectid"
                    class="form-control"
                    required
                  />
                </div>
                <div class="mb-3">
                  <label class="form-label">Credit</label>
                  <select v-model="formData.credit"
                    class="form-control">
                    <option value="3">3</option>
                    <option value="2">2</option>
                    <option value="1">1</option>
                  </select>
                </div>
                <div class="mb-3">
                  <label class="form-label">Grade</label>
                  <select v-model="formData.grade"
                  class="form-control">
                    <option value="A">A</option>
                    <option value="B+">B+</option>
                    <option value="B">B</option>
                    <option value="C+">C+</option>
                    <option value="C">C</option>
                    <option value="D+">D+</option>
                    <option value="D">D</option>
                    <option value="F">F</option>
                  </select>
                </div>
                <button type="submit" class="btn btn-success w-100">
                  {{ isEditing ? "บันทึกการแก้ไข" : "เพิ่มข้อมูล" }}
                </button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "Transcript",
  data() {
    return {
      formData: {
        subjectname: "",
        subjectid: "",
        credit: "",
        grade: ""
      },
      items: [],
      isEditing: false,
      currentItem: null
    };
  },
  methods: {
    async fetchItems() {
      try {
        const response = await fetch("http://localhost:3000/items", {
          method: "GET",
          headers: {
            "Content-Type": "application/json"
          }
        });
        if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
        this.items = await response.json();
      } catch (err) {
        console.error("Error fetching data:", err);
        alert("เกิดข้อผิดพลาดในการโหลดข้อมูล");
      }
    },
    resetForm() {
      this.formData = {
        subjectname: "",
        subjectid: "",
        credit: "",
        grade: ""
      };
      this.isEditing = false;
      this.currentItem = null;
    },
    editRow(item) {
      this.formData = { ...item };
      this.isEditing = true;
      this.currentItem = item;
      this.showModal();
    },
    async deleteRow(item) {
      if (!item.id) {
        alert("ไม่สามารถลบได้: ไม่พบ ID ของรายการ");
        return;
      }
      if (confirm("คุณต้องการลบรายการนี้ใช่หรือไม่?")) {
        try {
          const response = await fetch(`http://localhost:3000/items/${item.id}`, {
            method: "DELETE",
            headers: {
              "Content-Type": "application/json"
            }
          });
          if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
          this.items = this.items.filter(i => i.id !== item.id);
        } catch (err) {
          console.error("Error deleting data:", err);
          alert("เกิดข้อผิดพลาดในการลบข้อมูล");
        }
      }
    },
    async saveData() {
      try {
        // payload ไม่ต้องมี id เมื่อสร้างใหม่ (ให้ backend จัดการ)
        const payload = {
          subjectname: this.formData.subjectname,
          subjectid: this.formData.subjectid,
          credit: parseInt(this.formData.credit),
          grade: this.formData.grade,
        };

        let response;
        if (this.isEditing && this.currentItem && this.currentItem.id) {
          // แก้ไขข้อมูล
          response = await fetch(`http://localhost:3000/items/${this.currentItem.id}`, {
            method: "PUT",
            headers: {
              "Content-Type": "application/json",
              "Accept": "application/json"
            },
            body: JSON.stringify(payload)
          });
          
          if (!response.ok) {
            const errorText = await response.text();
            throw new Error(`HTTP error! status: ${response.status}, message: ${errorText}`);
          }

          const updatedItem = await response.json();
          const index = this.items.findIndex(item => item.id === this.currentItem.id);
          if (index !== -1) {
            this.items[index] = updatedItem; // อัพเดทข้อมูลใน array
          }
        } else {
          // เพิ่มข้อมูลใหม่
          response = await fetch("http://localhost:3000/items", {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
              "Accept": "application/json"
            },
            body: JSON.stringify(payload)
          });

          if (!response.ok) {
            const errorText = await response.text();
            throw new Error(`HTTP error! status: ${response.status}, message: ${errorText}`);
          }

          const newItem = await response.json();
          this.items.push(newItem);
        }
        
        this.hideModal();
        this.resetForm();
      } catch (err) {
        console.error("Error saving data:", err);
        alert(`เกิดข้อผิดพลาดในการบันทึกข้อมูล: ${err.message}`);
      }
    },
    showModal() {
      const modal = new bootstrap.Modal(document.getElementById("addModal"));
      modal.show();
    },
    hideModal() {
      const modalElement = document.getElementById("addModal");
      const modalInstance = bootstrap.Modal.getInstance(modalElement);
      modalInstance.hide();
    }
  },
  mounted() {
    this.fetchItems();
  }
};
</script>


<style scoped>
.modal-content {
  border-radius: 10px;
}
</style>