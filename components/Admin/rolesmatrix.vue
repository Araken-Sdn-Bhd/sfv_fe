<template>
  <div class="card mb-4">
    <div class="card-header bg-transparent">
      <h4>Akses Skrin</h4>
    </div>
    <div class="card-body">
      <ul class="nav sub-tab" id="nav-tab" role="tablist">
        <li class="nav-item">
          <a class="nav-link active" data-bs-toggle="tab" href="#nav-Module" role="tab" aria-controls="nav-Module"
            aria-selected="true"><i class="far fa-user-lock"></i> Tetapan 1: Akses Skrin</a>
        </li>
      </ul>
      <div class="tab-content" id="nav-tabContent">
        <div class="tab-pane fade show active" id="nav-Module" role="tabpanel">
      <form method="post" @submit.prevent="onAddroles">
        <div class="content-subtab">
          <div class="filter-form">
            <div class="row mt-3">
              <div class="col-sm-6 mb-3">
                <label class="form-label">Nama Modul</label>
                <select
                  v-model="ModuleId"
                  class="form-select"
                  aria-label="Default select example"
                  @change="onsubmodelbind($event)"
                >
                  <option value="0">Sila Pilih</option>
                  <option
                    v-for="mod in modulelist"
                    v-bind:key="mod.id"
                    v-bind:value="mod.id"
                  >
                    {{ mod.module_name }}
                  </option>
                </select>
              </div>

              <div class="col-sm-6 mb-3" v-show="IsSubmodule">
                <label class="form-label">Nama Sub Modul</label>
                <select
                  v-model="SubmoduleId"
                  class="form-select"
                  aria-label="Default select example"
                  @change="onchangescreen($event)"
                >
                  <option value="0">Sila Pilih</option>
                  <option
                    v-for="submod in submodulelist"
                    v-bind:key="submod.id"
                    v-bind:value="submod.id"
                  >
                    {{ submod.sub_module_name }}
                  </option>
                </select>
              </div>
            </div>
          </div>

          <table
            v-if="screenlist.length > 0"
            class="table table-striped data-table font-13 display nowrap"
            style="width: 100%"
          >
            <thead>
              <tr>
                <th>No</th>
                <th>Modul</th>
                <th>Sub Modul</th>
                <th>Nama Skrin</th>
                <th>Deskripsi</th>
                <th>Tindakan</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(scrn,index) in screenlist" :key="index">
                <td>{{ index+1 }}</td>
                <td>{{ scrn.module_name }}</td>
                <td>{{ scrn.sub_module_name }}</td>
                <td>{{ scrn.screen_name }}</td>
                <td>{{ scrn.screen_description }}</td>
                <td>
                  <input
                    class="form-check-input"
                    type="checkbox"
                    v-on:click="checkscreen(scrn.screen_id, $event)"
                  />
                </td>
              </tr>
            </tbody>
          </table>

          <div class="form-bottom">
            <div class="row">
              <div class="col-sm-6 mb-3">
                <label class="form-label">Nama</label>
                <select
                  v-model="staffId"
                  class="form-select"
                  aria-label="Default select example"
                >
                  <option value="0">Sila Pilih</option>
                  <option
                    v-for="stf in stafflist"
                    v-bind:key="stf.id"
                    v-bind:value="stf.id"
                  >
                    {{ stf.name }}
                  </option>
                </select>
              </div>
            </div>
            <!-- close-row -->
<p v-if="errors.length">
<ul>
        <li style="color:red"  v-for='err in errors'
    :key='err' >
          {{ err }}
        </li>
      </ul>
        </p>
        <br>
            <button class="btn btn-success pl-15" :class="SidebarAccess!=1?'hide':''">
              Simpan <i class="fal fa-arrow-from-left"></i>
            </button>
          </div>
        </div>
      </form>
    </div>
    </div>
    </div>
  </div>
</template>
<script>
export default {
  setup() {},
  data() {
    return {
      errors: [],
      ModuleId: 0,
      SubmoduleId: 0,
      staffId: 0,
      screenIds: "",
      screendetail: null,
      submodulelist: [],
      modulelist: [],
      screenlist: [],
      stafflist: [],
      selected: [],
      IsSubmodule: true,
      SidebarAccess: null,
    };
  },
  mounted() {},
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    this.SidebarAccess = JSON.parse(localStorage.getItem("SidebarAccess"));
    this.GetModuleList();
    this.getStaffList();
  },
  methods: {
    async checkscreen(value, event) {
      if (event.target.checked) {
        this.selected.push(value);
      } else {
        if (this.selected.indexOf(value) != -1)
          this.selected.splice(this.selected.indexOf(value), 1);
      }
    },
    async GetModuleList() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.get("screen-module/list", { headers });
      if (response.data.code == 200 || response.data.code == "200") {
        this.modulelist = response.data.list;
      } else {
        this.modulelist = [];
      }
    },
    async onsubmodelbind(event) {
      this.IsSubmodule = true;
      this.selected = [];
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "screen-module/sub-module-list-by-module-id",
        { module_id: event.target.value },
        { headers }
      );
      console.log("my submod list", response.data);
      if (response.data.code == 200 || response.data.code == "200") {
        this.submodulelist = response.data.list;
      } else {
        this.IsSubmodule = false;
        this.submodulelist = [];
      }
    },
    async onchangescreen(event) {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "screen-module/getScreenPageListByModuleIdAndSubModuleId",
        {
          module_id: this.ModuleId,
          sub_module_id: event.target.value,
        },
        { headers }
      );
      console.log("my screen list", response.data);
      if (response.data.code == 200 || response.data.code == "200") {
        this.screenlist = response.data.list;
      } else {
        this.screenlist = [];
      }
    },
    // async onHospitalCodechange(event) {
    //   const headers = {
    //     Authorization: "Bearer " + this.userdetails.access_token,
    //     Accept: "application/json",
    //     "Content-Type": "application/json",
    //   };
    //   const response = await this.$axios.post(
    //     "hospital/get-branch-by-hospital-code",
    //     {
    //       hospital_code: event.target.value,
    //     },
    //     { headers }
    //   );
    //   if (response.data.code == 200 || response.data.code == "200") {
    //     this.branchlist = response.data.branches;
    //   } else {
    //     this.branchlist = [];
    //   }
    // },
    // async onchangebranch(event) {
    //   const headers = {
    //     Authorization: "Bearer " + this.userdetails.access_token,
    //     Accept: "application/json",
    //     "Content-Type": "application/json",
    //   };
    //   const response = await this.$axios.get(
    //     "service/getServiceListByBranch?branchId=" + event.target.value,
    //     {
    //       headers,
    //     }
    //   );
    //   if (response.data.code == 200 || response.data.code == "200") {
    //     this.teamlist = response.data.list;
    //   } else {
    //     this.teamlist = [];
    //   }

    // },

    async getStaffList(){
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response1 = await this.$axios.post(
        "staff-management/getAllStaff",
        {  },
        {
          headers,
        }
      );
      if (response1.data.code == 200 || response1.data.code == "200") {
        this.stafflist = response1.data.list;
      } else {
        this.stafflist = [];
      }

    },
    // async GethospitalList() {
    //   const headers = {
    //     Authorization: "Bearer " + this.userdetails.access_token,
    //     Accept: "application/json",
    //     "Content-Type": "application/json",
    //   };
    //   const response = await this.$axios.get("hospital/list", {
    //     headers,
    //   });
    //   if (response.data.code == 200 || response.data.code == "200") {
    //     this.hospitallist = response.data.list;
    //   } else {
    //     this.hospitallist = [];
    //   }
    // },

    async onAddroles() {
      this.errors = [];
      try {
        if (this.ModuleId <= 0) {
          this.errors.push("Module Name  is required.");
        }
        if (!this.staffId) {
          this.errors.push("Name  is required.");
        }
        if (this.ModuleId && this.staffId) {
          const headers = {
            Authorization: "Bearer " + this.userdetails.access_token,
            Accept: "application/json",
            "Content-Type": "application/json",
          };
          if (this.selected.length > 0) {
            this.selected.forEach((value, index) => {
              if (!this.screenIds) {
                this.screenIds = value;
              } else {
                this.screenIds = this.screenIds + "," + value;
              }
            });
          }
          const response = await this.$axios.post(
            "screen-module/assign-screen",
            {
              module_id: this.ModuleId,
              screen_ids: this.screenIds.toString(),
              sub_module_id: this.SubmoduleId,
              added_by: this.userdetails.user.id,
              staff_id: this.staffId,
            },
            { headers }
          );

          console.log("my response", response.data);
          if (response.data.code == 200 || response.data.code == "200") {
            this.$swal.fire('created successfully', '', 'success');
            this.ResetModel();
          } else {
            this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + JSON.stringify(response.data.message),
                  footer: ''
                });
          }
        }
      } catch (e) {
        this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + e,
                  footer: ''
                });
      }
    },
    async ResetModel() {
      this.ModuleId = 0;
      this.SubmoduleId = 0;
      this.staffId = 0;
      this.selected = [];
      this.screenIds = "";
      this.screenlist = [];
    },
  },
};
</script>
