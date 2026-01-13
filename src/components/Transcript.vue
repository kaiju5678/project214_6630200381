<template>
  <section
    id="transcript"
    class="min-vh-100 d-flex align-items-center py-5"
  >
    <div class="container">
      <div class="row mb-4">
        <div class="col-12 text-center">
          <h2 class="text-white fw-bold display-5">Academic Transcript</h2>
          <p class="text-white-50">Manage your subjects and grades</p>
        </div>
      </div>

      <div class="card bg-dark border-secondary shadow-lg rounded-4 overflow-hidden">
        <div class="card-header bg-transparent border-secondary d-flex justify-content-between align-items-center p-4">
            <h5 class="text-white mb-0"><i class="fa-solid fa-list me-2"></i>Subject List</h5>
             <button
                class="btn btn-primary rounded-pill px-4"
                data-bs-toggle="modal"
                data-bs-target="#addModal"
                @click="resetForm"
              >
                <i class="fa-solid fa-plus me-2"></i>Add Subject
              </button>
        </div>
        
        <div class="card-body p-0">
            <div class="table-responsive">
                <table class="table table-dark table-hover mb-0 align-middle">
                    <thead class="bg-secondary text-uppercase text-secondary">
                    <tr>
                        <th class="ps-4">No.</th>
                        <th>Subject Code</th>
                        <th>Subject Name</th>
                        <th>Credit</th>
                        <th>Grade</th>
                        <th class="text-end pe-4">Actions</th>
                    </tr>
                    </thead>
                    <tbody>
                    <tr v-for="(item, index) in items" :key="item.id || index">
                        <td class="ps-4 text-white-50">{{ index + 1 }}</td>
                        <td class="fw-mono text-info">{{ item.subjectid }}</td>
                        <td>{{ item.subjectname }}</td>
                        <td><span class="badge bg-secondary rounded-pill">{{ item.credit }}</span></td>
                        <td>
                            <span :class="['badge rounded-pill', getGradeColor(item.grade)]" style="width: 40px;">
                                {{ item.grade }}
                            </span>
                        </td>
                        <td class="text-end pe-4">
                        <button
                            class="btn btn-outline-warning btn-sm me-2 rounded-circle"
                            @click="editRow(item)"
                            title="Edit"
                        >
                            <i class="fa-solid fa-pen"></i>
                        </button>
                        <button class="btn btn-outline-danger btn-sm rounded-circle" @click="deleteRow(item)" title="Delete">
                            <i class="fa-solid fa-trash"></i>
                        </button>
                        </td>
                    </tr>
                    <tr v-if="items.length === 0">
                        <td colspan="6" class="text-center py-5 text-white-50">
                            No data available. Please add a subject.
                        </td>
                    </tr>
                    </tbody>
                </table>
            </div>
        </div>
      </div>

      <div class="modal fade" id="addModal" tabindex="-1" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered">
          <div class="modal-content bg-dark text-white border-secondary">
            <div class="modal-header border-secondary">
              <h5 class="modal-title">
                {{ isEditing ? "Edit Subject" : "Add New Subject" }}
              </h5>
              <button
                type="button"
                class="btn-close btn-close-white"
                data-bs-dismiss="modal"
              ></button>
            </div>
            <div class="modal-body">
              <form @submit.prevent="saveData">
                <div class="mb-3">
                  <label class="form-label text-secondary">Subject ID</label>
                  <input
                    type="text"
                    v-model="formData.subjectid"
                    class="form-control bg-dark border-secondary text-white"
                    placeholder="e.g. 01418111"
                    required
                  />
                </div>
                <div class="mb-3">
                  <label class="form-label text-secondary">Subject Name</label>
                  <input
                    type="text"
                    v-model="formData.subjectname"
                    class="form-control bg-dark border-secondary text-white"
                    placeholder="e.g. Computer Programming"
                    required
                  />
                </div>
                <div class="row">
                    <div class="col-md-6 mb-3">
                        <label class="form-label text-secondary">Credit</label>
                        <select v-model="formData.credit" class="form-select bg-dark border-secondary text-white">
                            <option value="3">3</option>
                            <option value="2">2</option>
                            <option value="1">1</option>
                        </select>
                    </div>
                    <div class="col-md-6 mb-3">
                        <label class="form-label text-secondary">Grade</label>
                        <select v-model="formData.grade" class="form-select bg-dark border-secondary text-white">
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
                </div>
                <button type="submit" class="btn btn-success w-100 mt-2">
                  {{ isEditing ? "Update Subject" : "Save Subject" }}
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
        credit: "3",
        grade: "A"
      },
      // 1. ใส่ข้อมูล Mock Data จาก db.json มาไว้ตรงนี้เลย
      items: [
        { id: 1, subjectid: "01418111", subjectname: "Computer Programming", credit: 3, grade: "A" },
        { id: 2, subjectid: "01418112", subjectname: "Computer Programming Lab", credit: 1, grade: "A" },
        { id: 3, subjectid: "01418113", subjectname: "Calculus I", credit: 3, grade: "B+" },
        { id: 4, subjectid: "01418114", subjectname: "Digital Logic", credit: 3, grade: "B" }
      ],
      isEditing: false,
      currentItem: null
    };
  },
  methods: {
    getGradeColor(grade) {
        if (grade === 'A') return 'bg-success';
        if (grade === 'B+' || grade === 'B') return 'bg-primary';
        if (grade === 'C+' || grade === 'C') return 'bg-warning text-dark';
        if (grade === 'D+' || grade === 'D') return 'bg-orange';
        if (grade === 'F') return 'bg-danger';
        return 'bg-secondary';
    },
    // 2. ลบ fetchItems ของเดิมทิ้ง เพราะเรามีข้อมูลใน data() แล้ว
    fetchItems() {
      // ไม่ต้องทำอะไร หรืออาจจะทำ Loading effect เล่นๆ ก็ได้
      console.log("Mock data loaded");
    },
    resetForm() {
      this.formData = { subjectname: "", subjectid: "", credit: "3", grade: "A" };
      this.isEditing = false;
      this.currentItem = null;
    },
    editRow(item) {
      this.formData = { ...item };
      this.isEditing = true;
      this.currentItem = item;
      this.showModal();
    },
    // 3. แก้ deleteRow ให้ลบจาก Array ในเครื่องแทน
    deleteRow(item) {
      if (confirm("Are you sure you want to delete this subject? (Demo Mode)")) {
        this.items = this.items.filter(i => i.id !== item.id);
      }
    },
    // 4. แก้ saveData ให้เพิ่ม/แก้ไข Array ในเครื่องแทน
    saveData() {
      const payload = {
        subjectname: this.formData.subjectname,
        subjectid: this.formData.subjectid,
        credit: parseInt(this.formData.credit),
        grade: this.formData.grade,
      };

      if (this.isEditing && this.currentItem) {
        // แก้ไขข้อมูลใน Array (หา index แล้วแทนที่)
        const index = this.items.findIndex(item => item.id === this.currentItem.id);
        if (index !== -1) {
            // รวม ID เดิมเข้ากับข้อมูลใหม่
            this.items[index] = { ...payload, id: this.currentItem.id };
        }
      } else {
        // เพิ่มข้อมูลใหม่ (Generate ID เองมั่วๆ)
        const newId = this.items.length > 0 ? Math.max(...this.items.map(i => i.id)) + 1 : 1;
        this.items.push({ ...payload, id: newId });
      }
      
      this.hideModal();
      this.resetForm();
    },
    showModal() {
      const modal = new bootstrap.Modal(document.getElementById("addModal"));
      modal.show();
    },
    hideModal() {
      const el = document.getElementById("addModal");
      const modal = bootstrap.Modal.getInstance(el);
      modal.hide();
    }
  },
  mounted() {
    // เรียกใช้งานตอนเปิดหน้าเว็บ
    this.fetchItems();
  }
};
</script>

<style scoped>
#transcript {
  /* เปลี่ยนตรงนี้! ใช้ตัวแปรแทนสี #121212 */
  background-color: var(--section-bg-2);
  transition: background-color 0.4s ease;
}

/* ... CSS อื่นๆ ... */
.fw-mono {
    font-family: 'Courier New', Courier, monospace;
    font-weight: bold;
}
.bg-orange {
    background-color: #fd7e14;
}
</style>