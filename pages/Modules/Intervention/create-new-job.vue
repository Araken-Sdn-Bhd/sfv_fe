<template>
  <div id="layoutSidenav">
    <CommonSidebar  />
    <div id="layoutSidenav_content">
      <CommonHeader />
      <main>
        <Loader v-if="loader"/>
        <div class="container-fluid px-4">
          <div class="page-title">
            <h1>Job Offer Form</h1>
            <a class="add-btn"><i class="fal fa-plus"></i></a>
          </div>
          <div class="card mb-4">
            <div class="card-header icon-title">
              <a href="#"><i class="fa fa-shield-alt"></i></a>
              <h4>Create New Job</h4>
            </div>
            <div class="card-body">
              <form class="mt-3" method="post" @submit.prevent="OnCreateJob">
                <div class="row mb-3">
                  <label for="inputEmail3" class="col-sm-4 col-form-label"
                    >Position Offered</label
                  >
                  <div class="col-sm-8">
                    <input
                      type="text"
                      class="form-control"
                      id="inputEmail3"
                      v-model="position_offered"
                    />
                  </div>
                </div>
                <!-- row -->
                <div class="row mb-3">
                  <label for="inputEmail3" class="col-sm-4 col-form-label"
                    >Location of Position Offered</label
                  >
                  <div class="col-sm-8">
                    <input
                      type="text"
                      class="form-control mb-2"
                      v-model="position_location_1"
                    />
                    <input
                      type="text"
                      class="form-control mb-2"
                      v-model="position_location_2"
                    />
                    <input
                      type="text"
                      class="form-control mb-2"
                      v-model="position_location_3"
                    />
                  </div>
                </div>
                <!-- row -->
                <div class="row mb-3">
                  <label for="inputEmail3" class="col-sm-4 col-form-label"
                    >Minimum Education</label
                  >
                  <div class="col-sm-8">
                    <select class="form-select" v-model="education_id">
                      <option value="0">Select Minimum Education</option>
                      <option
                        v-for="edu in educationlist"
                        v-bind:key="edu.id"
                        v-bind:value="edu.id"
                      >
                        {{ edu.section_value }}
                      </option>
                    </select>
                  </div>
                </div>
                <!-- row -->
                <div class="row mb-3 align-items-center">
                  <label for="inputEmail3" class="col-sm-4 col-form-label"
                    >Duration of Employment</label
                  >
                  <div class="col-sm-5">
                    <input
                      type="text"
                      class="form-control"
                      id="inputEmail3"
                      v-model="duration_of_employment"
                    />
                  </div>
                  <div class="col-sm-3">month(s)</div>
                </div>
                <!-- row -->
                <div class="row mb-3 align-items-center">
                  <label for="inputEmail3" class="col-sm-4 col-form-label"
                    >Average salary offered</label
                  >
                  <div class="col-sm-1">RM</div>
                  <div class="col-sm-4">
                    <input
                      type="text"
                      class="form-control"
                      id="inputEmail3"
                      v-model="salary_offered"
                    />
                  </div>
                  <div class="col-sm-3">per month</div>
                </div>
                <!-- row -->
                <div class="row mb-3">
                  <label for="inputEmail3" class="col-sm-4 col-form-label"
                    >Work Schedule</label
                  >
                  <div class="col-sm-8">
                    <div class="form-check form-check-inline">
                      <input
                        class="form-check-input"
                        type="checkbox"
                        value="Part time"
                        id="flexCheckDefault"
                        @change="changeschedule('Part time')"
                      />
                      <label class="form-check-label" for="flexCheckDefault">
                        Part time
                      </label>
                    </div>
                    <div class="form-check form-check-inline">
                      <input
                        class="form-check-input"
                        type="checkbox"
                        value="Full-time"
                        id="flexCheckChecked"
                        @change="changeschedule('Full-time')"
                      />
                      <label class="form-check-label" for="flexCheckChecked">
                        Full-time
                      </label>
                    </div>
                  </div>
                </div>
                <!-- row -->
                <div class="row mb-3">
                  <label for="inputEmail3" class="col-sm-4 col-form-label"
                    >Does your company provide transport?</label
                  >
                  <div class="col-sm-8">
                    <div class="form-check form-check-inline">
                      <input
                        class="form-check-input"
                        type="radio"
                        name="inlineRadioOptions"
                        id="inlineRadio1"
                        value="1"
                        v-model="is_transport"
                      />
                      <label class="form-check-label" for="inlineRadio1"
                        >Yes</label
                      >
                    </div>
                    <div class="form-check form-check-inline">
                      <input
                        class="form-check-input"
                        type="radio"
                        name="inlineRadioOptions"
                        id="inlineRadio2"
                        value="0"
                        v-model="is_transport"
                      />
                      <label class="form-check-label" for="inlineRadio2"
                        >No</label
                      >
                    </div>
                  </div>
                </div>
                <!-- row -->
                <div class="row mb-3">
                  <label for="inputEmail3" class="col-sm-4 col-form-label"
                    >Does your company provide accommodation?</label
                  >
                  <div class="col-sm-8">
                    <div class="form-check form-check-inline">
                      <input
                        class="form-check-input"
                        type="radio"
                        name="inlineRadioOption"
                        id="inlineRadio11"
                        value="1"
                        v-model="is_accommodation"
                      />
                      <label class="form-check-label" for="inlineRadio11"
                        >Yes</label
                      >
                    </div>
                    <div class="form-check form-check-inline">
                      <input
                        class="form-check-input"
                        type="radio"
                        name="inlineRadioOption"
                        id="inlineRadio22"
                        value="0"
                        v-model="is_accommodation"
                      />
                      <label class="form-check-label" for="inlineRadio22"
                        >No</label
                      >
                    </div>
                  </div>
                </div>
                <!-- row -->
                <div class="row mb-3">
                  <label for="inputEmail3" class="col-sm-4 col-form-label"
                    >Work Requirement</label
                  >
                  <div class="col-sm-8 box-wr">
                    <div class="form-check">
                      <input
                        class="form-check-input"
                        type="checkbox"
                        v-model="labour" value="Labour (Heavy Lifting)"
                        @change="
                          changeworkrequirement('Labour (Heavy Lifting)')
                        "
                        id="flexCheck1"
                      />
                      <label class="form-check-label" for="flexCheck1">
                        Labour (Heavy Lifting)
                      </label>
                    </div>
                    <div class="form-check">
                      <input
                        class="form-check-input"
                        type="checkbox" v-model="goodfocus" value="Good Focus/Concentration"
                        @change="
                          changeworkrequirement('Good Focus/Concentration')
                        "
                        id="flexCheck2"
                      />
                      <label class="form-check-label" for="flexCheck2">
                        Good Focus/Concentration
                      </label>
                    </div>
                    <div class="form-check">
                      <input
                        class="form-check-input"
                        type="checkbox" v-model="communication" value="Communication Skills"
                        @change="changeworkrequirement('Communication Skills')"
                        id="flexCheck3"
                      />
                      <label class="form-check-label" for="flexCheck3">
                        Communication Skills
                      </label>
                    </div>
                    <div class="form-check">
                      <input
                        class="form-check-input"
                        type="checkbox" v-model="reading" value="Reading"
                        @change="changeworkrequirement('Reading')"
                        id="flexCheck4"
                      />
                      <label class="form-check-label" for="flexCheck4">
                        Reading
                      </label>
                    </div>
                    <div class="form-check">
                      <input
                        class="form-check-input"
                        type="checkbox" v-model="calculation" value="Calculation"
                        @change="changeworkrequirement('Calculation')"
                        id="flexCheck5"
                      />
                      <label class="form-check-label" for="flexCheck5">
                        Calculation
                      </label>
                    </div>
                    <div class="form-check">
                      <input
                        class="form-check-input"
                        type="checkbox"
                        value="other-wr" v-model="other"
                        id="flexCheck6"
                        @change="changeworkrequirement('Other')"
                      />
                      <label class="form-check-label" for="flexCheck6">
                        Other
                      </label>
                    </div>

                    <div class="other-wr hide">
                      <input
                        type="text"
                        placeholder="Please specify"
                        class="form-control"
                        v-model="workrequirementother"
                        name=""
                      />
                    </div>
                  </div>
                </div>
                <!-- row -->
                <div class="row mb-3">
                  <label for="inputEmail3" class="col-sm-4 col-form-label"
                    >MENTARI</label
                  >
                  <div class="col-sm-8">
                    <select class="form-select" v-model="branch_id">
                      <option value="0">Please Select</option>
                      <option
                        v-for="brnch in list"
                        v-bind:key="brnch.id"
                        v-bind:value="brnch.id"
                      >
                        {{ brnch.hospital_branch_name }}
                      </option>
                    </select>
                  </div>
                </div>
                   <div class="row mb-3">
                  <label for="inputEmail3" class="col-sm-4 col-form-label"
                    >Job Availability</label
                  >
                  <div class="col-sm-8">
                    <div class="form-check form-check-inline">
                      <input
                        class="form-check-input"
                        type="radio"
                        name="inlineRadioOptions"
                        id="inlineRadio111"
                        value="1"
                        v-model="job_availability"
                      />
                      <label class="form-check-label" for="inlineRadio111"
                        >Available</label
                      >
                    </div>
                    <div class="form-check form-check-inline">
                      <input
                        class="form-check-input"
                        type="radio"
                        name="inlineRadioOptions"
                        id="inlineRadio222"
                        value="0"
                        v-model="job_availability"
                      />
                      <label class="form-check-label" for="inlineRadio222"
                        >Not Available</label
                      >
                    </div>
                  </div>
                </div>
                 <p v-if="errorList.length">
                          <ul>
                           <li style="color:red"  v-for='err in errorList' :key='err' >
                           {{ err }}
                             </li>
                        </ul>
                       </p>
                <!-- row -->
                <div class="d-flex"  :class="SidebarAccess!=1?'hide':''">
                  <button
                    type="submit"
                    class="btn btn-warning btn-text ml-auto"
                  >
                    <i class="fa fa-save"></i> Save
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </main>
      <intervention-footer></intervention-footer>
    </div>
  </div>
</template>
<script>
import CommonHeader from '../../../components/CommonHeader.vue';
import CommonSidebar from '../../../components/CommonSidebar.vue';
export default {
  components: { CommonSidebar, CommonHeader },
  name: "create-new-job",
  data() {
    return {
      userdetails: null,
      list: [],
      errorList: [],
      educationlist: [],
      type: "add",
      company_id: 1,
      position_offered: "",
      position_location_1: "",
      position_location_2: "",
      position_location_3: "",
      education_id: 0,
      duration_of_employment: 0,
      salary_offered: "",
      work_schedule: "",
      is_transport: 0,
      is_accommodation: 0,
      work_requirement: "",
      branch_id: 0,
      job_availability: 1,
      workrequirementother: "",
      loader: false,
      labour: "",
      goodfocus: "",
      communication: "",
      reading: "",
      calculation: "",
      other: "",
      SidebarAccess:null,
    };
  },
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    this.SidebarAccess = JSON.parse(localStorage.getItem("SidebarAccess"));
    $('.box-wr input[type="checkbox"]').click(function () {
      var inputValue = $(this).attr("value");
      $("." + inputValue).toggle();
    });
    this.GetList();
  },
  methods: {
    async GetList() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.get("hospital/branch-list", {
        headers,
      });
      if (response.data.code == 200 || response.data.code == "200") {
        this.list = response.data.list;
      } else {
        this.list = [];
      }
      const response1 = await this.$axios.get(
        "general-setting/list?section=" + "education-level",
        { headers }
      );
      if (response1.data.code == 200 || response1.data.code == "200") {
        this.educationlist = response1.data.list;
      } else {
        this.educationlist = [];
      }
    },
    async OnCreateJob() {
      this.errorList = [];
      try {
        if (!this.position_offered) {
          this.errorList.push("Position Offered is required");
        }
        if (!this.position_location_1) {
          this.errorList.push("Location of Position Offered is required");
        }
        if (!this.education_id) {
          this.errorList.push("Minimum Education is required");
        }
        if (!this.duration_of_employment) {
          this.errorList.push("Duration of Employment is required");
        }
        if (!this.salary_offered) {
          this.errorList.push("Average salary offered is required");
        }
        if (!this.work_schedule) {
          this.errorList.push("Work Schedule is required");
        }
        if (!this.work_requirement) {
          this.errorList.push("Work Requirement is required");
        }
        if (!this.branch_id) {
          this.errorList.push("MENTARI is required");
        }
        if (
          this.position_offered &&
          this.position_location_1 &&
          this.education_id &&
          this.duration_of_employment &&
          this.salary_offered &&
          this.work_schedule &&
          this.work_requirement &&
          this.branch_id
        ) {
          this.loader = true;
          console.log("work requirement", this.work_requirement);
          const headers = {
            Authorization: "Bearer " + this.userdetails.access_token,
            Accept: "application/json",
            "Content-Type": "application/json",
          };
          const response = await this.$axios.post(
            "intervention-job/add",
            {
              added_by: this.userdetails.user.id,
              company_id: this.company_id,
              position_offered: this.position_offered,
              position_location_1: this.position_location_1,
              position_location_2: this.position_location_2,
              position_location_3: this.position_location_3,
              education_id: this.education_id,
              duration_of_employment: this.duration_of_employment,
              salary_offered: this.salary_offered,
              work_schedule: this.work_schedule,
              is_transport: this.is_transport,
              is_accommodation: this.is_accommodation,
              work_requirement: JSON.stringify([
                {
                  WorkRequirement: {
                    "Labour (Heavy Lifting)": this.labour,
                    "Good Focus/Concentration": this.goodfocus,
                    "Communication Skills": this.communication,
                    Reading: this.reading,
                    Calculation: this.calculation,
                    Other: this.workrequirementother,
                  },
                },
              ]),
              branch_id: this.branch_id,
              job_availability: this.job_availability,
              type: this.type,
            },
            { headers }
          );
          console.log("result", response.data);
          if (response.data.code == 200) {
            this.loader = false;
            this.$swal.fire('created successfully', '', 'success');
            this.$router.push("/modules/Intervention/list-of-job-offer");
          } else {
            this.loader = false;
            this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + JSON.stringify(response.data.message),
                  footer: ''
                });
          }
        }
      } catch (e) {
        this.loader = false;
      }
    },
    changeschedule(val) {
      this.work_schedule = val;
    },
    changeworkrequirement(val) {
      this.work_requirement = val;
    },
  },
};
</script>
<style scoped>
.hide {
  display: none !important;
}
</style>
