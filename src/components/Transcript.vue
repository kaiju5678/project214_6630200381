<template>
  <section
    id="transcript"
    class="min-vh-100 d-flex align-items-center py-5"
    style="background-color: #121212;"
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
      items: [],
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
    async fetchItems() {
      try {
        const response = await fetch("http://localhost:3000/items");
        if (!response.ok) throw new Error(`Status: ${response.status}`);
        this.items = await response.json();
      } catch (err) {
        console.error("Fetch error:", err);
      }
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
    async deleteRow(item) {
      if (!item.id) return;
      if (confirm("Are you sure you want to delete this subject?")) {
        try {
          await fetch(`http://localhost:3000/items/${item.id}`, { method: "DELETE" });
          this.items = this.items.filter(i => i.id !== item.id);
        } catch (err) { console.error(err); }
      }
    },
    async saveData() {
      try {
        const payload = {
          subjectname: this.formData.subjectname,
          subjectid: this.formData.subjectid,
          credit: parseInt(this.formData.credit),
          grade: this.formData.grade,
        };

        let response;
        if (this.isEditing && this.currentItem) {
          response = await fetch(`http://localhost:3000/items/${this.currentItem.id}`, {
            method: "PUT",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(payload)
          });
          const updatedItem = await response.json();
          const index = this.items.findIndex(item => item.id === this.currentItem.id);
          if (index !== -1) this.items[index] = updatedItem;
        } else {
          response = await fetch("http://localhost:3000/items", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(payload)
          });
          const newItem = await response.json();
          this.items.push(newItem);
        }
        
        this.hideModal();
        this.resetForm();
      } catch (err) { console.error(err); }
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
    this.fetchItems();
  }
};
</script>

<style scoped>
.fw-mono {
    font-family: 'Courier New', Courier, monospace;
    font-weight: bold;
}
.bg-orange {
    background-color: #fd7e14;
}
</style>