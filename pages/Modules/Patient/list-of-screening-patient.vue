<template>
  <div id="layoutSidenav">
    <CommonSidebar />
    <div id="layoutSidenav_content">
      <CommonHeader />
      <main>
        <div class="container-fluid px-4">
          <div class="page-title">
            <h1>List of Screening Patient</h1>
          </div>

          <div class="card mb-4">
            <div class="card-body">
              <div class="search-table">
                <div class="row">
                  <div class="col-lg-4 col-sm-6 mt-2 mb-3">
                    <select
                      v-model="branch"
                      v-if="dataReady"
                      disabled
                      class="form-select"
                      aria-label="Default select example" @change="OnSearch"
                    >
                      <option v-bind:value="0">Select Branch</option>
                      <option
                        v-for="hst in branchlist"
                        v-bind:key="hst.id"
                        v-bind:value="hst.id"
                      >
                        {{ hst.hospital_branch_name }}
                      </option>
                    </select>
                    <select
                      v-model="branch"
                      v-if="dataReady2"
                      class="form-select"
                      aria-label="Default select example" @change="OnSearch"
                    >
                      <option v-bind:value="0">Select Branch</option>
                      <option
                        v-for="hst in branchlist"
                        v-bind:key="hst.id"
                        v-bind:value="hst.id"
                      >
                        {{ hst.hospital_branch_name }}
                      </option>
                    </select>
                  </div>
                </div>
              </div>
              <!-- search-table -->

              <div style="overflow-x:auto;">
                <table class="table table-striped data-table display nowrap" style="width: 100%">
                <thead>
                  <tr>
                    <th>No</th>
                    <th>MRN</th>
                    <th>SALUTATION</th>
                    <th>Name</th>
                    <th>Age</th>
                    <th>NRIC/Passport</th>
                    <th>Assigned Doctor</th>
                    <th>Services</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(patint, index) in list" :key="index">
                    <td>{{ index+1 }}</td>
                    <td>{{ patint.patient_mrn }}</td>
                    <td>{{ patint.salutation }}</td>
                    <td>
                      <a
                        style="color: #18846f; cursor: pointer"
                        @click="oneditPatient(patint.id)"
                        >{{ patint.name_asin_nric }}</a
                      >
                    </td>
                    <td>{{ patint.age }}</td>
                    <td>{{ patint.nric_id }}</td>
                    <td>{{ patint.team_name }}</td>
                    <td>{{ patint.service }}</td>
                  </tr>
                </tbody>
              </table>
              </div>

            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>
<script>
import CommonHeader from '../../../components/CommonHeader.vue';
import CommonSidebar from '../../../components/CommonSidebar.vue';
export default {
  components: { CommonSidebar, CommonHeader },
  name: "book-appointment",
  data() {
    return {
      userdetails: null,
      list: [],
      branchlist: [],
      branch: 0,
      dataReady: false,
      dataReady2: false,
    };
  },
  beforeMount() {
    this.SidebarAccess = JSON.parse(localStorage.getItem("SidebarAccess"));
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    this.GetBranchList();
    this.getRole();
  },
   mounted() {
    const headers = {
      Authorization: "Bearer " + this.userdetails.access_token,
      Accept: "application/json",
      "Content-Type": "application/json",
    };
    const axios = require("axios").default;
    axios
      .post(
        `${this.$axios.defaults.baseURL}`+"patient-registration/getPatientRegistrationListByScreening",
        {email:this.userdetails.user.email,branch_id:this.userdetails.branch.branch_id },
        { headers }
      )
      .then((resp) => {
        this.list = resp.data.list;
        $(document).ready(function () {
          // $(".data-table").DataTable({
          //   searching: false,
          //   bLengthChange: false,
          //   bInfo: false,
          //   // autoWidth: false,
          //   // responsive: true,
          //   scrollX: true,
          //   language: {
          //     paginate: {
          //       next: '<i class="fad fa-arrow-to-right"></i>', // or '→'
          //       previous: '<i class="fad fa-arrow-to-left"></i>', // or '←'
          //     },
          //   },
          // });
        });
      })
      .catch ((err) => {
        this.loader = false;
        this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + err,
                  footer: ''
                });

        console.error(err);
      });
  },
  methods: {
    async getRole() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "staff-management/getRoleCode",
        { email: this.userdetails.user.email },
        {
          headers,
        }
      );
      this.branch=this.userdetails.branch.branch_id;
            if (response.data.list.code =="superadmin"){
              this.dataReady2= true;
              this.dataReady= false;
            }else{
              this.dataReady= true;
              this.dataReady2= false;
            }

    },
    async GetBranchList() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.get("hospital/branch-list", {
        headers,
      });
      if (response.data.code == 200 || response.data.code == "200") {
        this.branchlist = response.data.list;
      } else {
        this.branchlist = [];
      }
    },
    oneditPatient(Id) {
      if(this.SidebarAccess==1){
        this.$router.push({
        path: "/modules/Intervention/patient-summary-patient",
        query: { id: Id },
      });
      }else{
      }
    },
     async OnSearch() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      if (!this.keyword) {
        this.keyword = "no-keyword";
      }
      const response = await this.$axios.post(
        "/patient/search",
        {
          keyword: "no-keyword",
          branch_id: this.branch,
          service_id: 0,
        },
        { headers }
      );
      console.log("my list", response.data);
      if (response.data.code == 200) {
        this.list = response.data.list;
      } else {
        this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + this.error,
                  footer: ''
                });
      }
    },
  },
};
</script>
