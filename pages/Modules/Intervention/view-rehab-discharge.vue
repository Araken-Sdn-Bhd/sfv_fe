<template>
  <div id="layoutSidenav">
    <CommonSidebar  />
    <div id="layoutSidenav_content">
      <CommonHeader />
      <main>
        <div class="container-fluid px-4">
          <div class="page-title">
            <h1>REHAB DISCHARGE NOTE</h1>
            <!-- <a href="#"><i class="fal fa-plus"></i> Add</a> -->
          </div>
          <div class="card mb-4">
            <div class="card-body">
              <div>
                <div class="row">
                  <div class="col-sm-6">
                    <div class="mb-3">
                      <label class="form-label">Name<small style="color:red">*</small> </label>
                      <input type="text" class="form-control" v-model="name" disabled />
                    </div>
                  </div>
                  <div class="col-sm-6">
                    <div class="mb-3">
                      <label class="form-label">MRN<small style="color:red">*</small> </label>
                      <input type="text" class="form-control" v-model="mrn"  disabled/>
                    </div>
                  </div>
                </div>
                <!-- close-row -->
                <div class="row">
                  <div class="col-sm-6">
                    <div class="mb-3">
                      <label class="form-label">Date<small style="color:red">*</small> </label>
                      <input type="date" class="form-control" v-model="date" disabled/>
                    </div>
                  </div>
                  <div class="col-sm-6">
                    <div class="mb-3">
                      <label class="form-label">Time<small style="color:red">*</small> </label>
                      <input type="time" class="form-control" v-model="time" disabled />
                    </div>
                  </div>
                </div>
                <!-- close-row -->
                <div class="row">
                  <div class="col-sm-6">
                    <div class="mb-3">
                      <label class="form-label">Staff Name<small style="color:red">*</small> </label>
                      <input type="text" class="form-control" v-model="staff_name" disabled />
                    </div>
                  </div>
                  <div class="col-sm-6">
                    <div class="mb-3">
                      <label class="form-label">Diagnosis<small style="color:red">*</small> </label>
                      <select class="form-select" v-model="type_diagnosis_id" disabled>
                       <option value="0">Select Diagnosis</option>
                                <option
                          v-for="catcode in diagonisislist"
                          v-bind:key="catcode.id"
                          v-bind:value="catcode.id"
                        >
                        {{ catcode.icd_code }} {{catcode.icd_name}}
                        </option>
                      </select>
                    </div>
                  </div>
                </div>
                <!-- close-row -->
                <div class="row">
                  <div class="col-sm-12">
                    <label class="form-label">Intervention<small style="color:red">*</small> </label>
                    <div class="mb-3">
                      <div class="form-check form-check-inline" >
                        <input
                          class="form-check-input"
                          type="radio"
                          id="inlineCheckbox1"
                          value="supportedEmployment"
                          name="inlineRadioOptions" v-model="intervention" disabled
                        />
                        <label class="form-check-label" for="inlineCheckbox1"
                          >Supported Employment<small style="color:red">*</small> </label
                        >
                      </div>
                      <div class="form-check form-check-inline">
                        <input
                          class="form-check-input"
                          type="radio"
                          id="inlineCheckbox2"
                          value="ETP"
                          name="inlineRadioOptions" v-model="intervention" disabled
                        />
                        <label class="form-check-label" for="inlineCheckbox2"
                          >ETP</label
                        >
                      </div>
                      <div class="form-check form-check-inline">
                        <input
                          class="form-check-input"
                          type="radio"
                          id="inlineCheckbox3"
                          value="jobClub"
                          name="inlineRadioOptions" v-model="intervention" disabled
                        />
                        <label class="form-check-label" for="inlineCheckbox3"
                          >Job Club</label
                        >
                      </div>
                    </div>
                  </div>
                </div>
                <!-- close-row -->
                <div class="row">
                  <div class="col-sm-6">
                    <div class="mb-3">
                      <label class="form-label">Category of Discharge<small style="color:red">*</small> </label>
                      <select class="form-select" v-model="discharge_category" disabled>
                        <option value="0">Please Select</option>
                                                <option
              v-for="dis in dischargelist"
              v-bind:key="dis.id"
              v-bind:value="dis.id"
            >
              {{ dis.name }}
            </option>
                      </select>
                    </div>
                  </div>
                </div>
                <!-- close-row -->
                <div class="row">
                  <div class="col-sm-12">
                    <div class="mb-3">
                      <label class="form-label">Comment<small style="color:red">*</small> </label>
                      <textarea class="form-control" placeholder="Enter Description" rows="15" v-model="comment" disabled></textarea>
                    </div>
                  </div>
                </div>
                <!-- close-row -->
              <div
                  class="accordion form-accordion mt-3"
                  id="accordionExample"
                >
                  <div class="accordion-item">
                    <h2 class="accordion-header" id="headingOne">
                      <button
                        class="accordion-button"
                        type="button"
                        data-bs-toggle="collapse"
                        data-bs-target="#collapseOne"
                        aria-expanded="true"
                        aria-controls="collapseOne"
                      >
                        OCCASION OF SERVICES
                      </button>
                    </h2>
                    <div
                      id="collapseOne"
                      class="accordion-collapse collapse show"
                      aria-labelledby="headingOne"
                      data-bs-parent="#accordionExample"
                    >
                      <div class="accordion-body">
                        <div class="row mb-3">
                          <label class="col-sm-4 col-form-label"
                            >Location Of Services<small style="color:red">*</small> </label
                          >
                          <div class="col-sm-8">
                            <select
                              class="form-select"
                              v-model="location_services" disabled
                            >
                              <option value="0">
                                Select location of services
                              </option>
                             <option
                                  v-for="loc in locationlist"
                                  v-bind:key="loc.id"
                                  v-bind:value="loc.id"
                                >
                                  {{ loc.section_value }}
                                </option>
                            </select>
                          </div>
                        </div>
                        <!-- close-row -->
                        <div class="row mb-3">
                          <label class="col-sm-4 col-form-label"
                            >Type Of Diagnosis<small style="color:red">*</small> </label
                          >
                          <div class="col-sm-8">
                            <select class="form-select" v-model="type_diagnosis_id" disabled>
                                <option value="0">Select Diagnosis</option>
                                <option
              v-for="catcode in diagonisislist"
              v-bind:key="catcode.id"
              v-bind:value="catcode.id"
            >
            {{ catcode.icd_code }} {{catcode.icd_name}}
            </option>
                              </select>
                          </div>
                        </div>
                        <div class="row mb-3 align-items-flex-start">
                      <label class="col-sm-4 col-form-label">Additional Type Of Diagnosis</label>
                      <div class="col-sm-8 align-items-flex-start" >
                          <select
                          id="additionalbox" 
                          class="form-select multiselect" multiple="multiple" disabled>
                              <option value="0">Please Select</option><option
                              v-for="catcode in diagonisislist"
                              v-bind:key="catcode.id"
                              v-bind:value="catcode.id">
                            {{ catcode.icd_code }} {{catcode.icd_name}}
                            </option>
                        </select>
                      </div>
                    </div>
                  
                        <!-- close-row -->
                        <div class="row mb-3">
                          <label class="col-sm-4 col-form-label"
                            >Category Of Services<small style="color:red">*</small>
                          </label>
                          <div class="col-sm-8">
                            <div class="form-check form-check-inline" >
                              <input
                                class="form-check-input"
                                type="radio"
                                name="inlineRadioOptions1"
                                id="inlineRadio1"
                                value="assisstance"
                                v-model="category_services" disabled
                              /> 
                              <label class="form-check-label" for="inlineRadio1"
                                >Assisstance / Supervision</label
                              >
                            </div>
                            <div class="form-check form-check-inline">
                              <input
                                class="form-check-input"
                                type="radio"
                                name="inlineRadioOptions1"
                                id="inlineRadio2"
                                value="clinical-work"
                                v-model="category_services" disabled
                              />
                              <label class="form-check-label" for="inlineRadio2"
                                >Clinical Work / Procedure
                              </label>
                            </div>
                            <div class="form-check form-check-inline">
                              <input
                                class="form-check-input"
                                type="radio"
                                name="inlineRadioOptions1"
                                id="inlineRadio3"
                                value="external"
                                v-model="category_services" disabled
                              />
                              <label class="form-check-label" for="inlineRadio3"
                                >External</label
                              >
                            </div>
                          </div>
                        </div>
                        <!-- close-row -->
                        <!-- hide-div -->
                        <div class="assisstance services hide mb-3">
                          <div class="row">
                            <div class="col-md-6 mb-3">
                              <label class="form-label">Services<small style="color:red">*</small> </label>
                              <select class="form-select" v-model="services_id" disabled>
                                 <option value="0">Select Service</option>
                      <option
                        v-for="slt in assistancelist"
                        v-bind:key="slt.id"
                        v-bind:value="slt.id"
                      >
                        {{ slt.section_value }}
                      </option>
                              </select>
                            </div>
                          </div>
                        </div>
                        <!-- 01 -->
                        <div class="clinical-work services hide mb-3">
                        <div class="row mb-6 align-items-flex-start">
                          <div class="col-md-4 mb-3">
                            <label class="form-label">ICD 9 CODE<small style="color:red">*</small> </label>
                            <select
                              class="form-select"
                              v-model="code_id"
                              disabled
                            >
                              <option value="0">Select code</option>
                              <option
                                v-for="type in codelist"
                                v-bind:key="type.id"
                                v-bind:value="type.id">
                               {{ type.icd_category_code }} {{type.icd_category_name}}
                              </option>
                            </select>
                          </div>

                          <div class="col-md-8 mb-3">
                          <div><label class="form-label">ICD 9 SUB CODE<small style="color:red">*</small> </label></div>
                          <div>
                          <div class="mt-2 align-items-flex-start">
                            <select
                              class="form-select multiselect" multiple="multiple"
                              id="sub_code_id" style="width:100%" disabled>

                              <option value="0">Select code</option>
                              <option
                                v-for="catcode in icdcatcodelist"
                                v-bind:key="catcode.id"
                                v-bind:value="catcode.id">
                                {{ catcode.icd_code }}{{catcode.icd_name}}
                              </option>
                            </select>
                          </div>
                          </div>
                          </div>

                         
                          
                        </div>

                        <!--additional code-->
                        <div class="row mb-6 align-items-flex-start">
                          <div class="col-md-4 mb-3">
                            <label class="form-label">Additional ICD 9 CODE</label>
                            <select
                              class="form-select"
                              v-model="add_code_id"
                              disabled
                            >
                              <option value="0">Select code</option>
                              <option
                                v-for="type in codelist"
                                v-bind:key="type.id"
                                v-bind:value="type.id">
                               {{ type.icd_category_code }} {{type.icd_category_name}}
                              </option>
                            </select>
                          </div>

                          <div class="col-md-8 mb-3">
                          <div><label class="form-label">Additional ICD 9 SUB CODE</label></div>
                          <div>
                          <div class="mt-2 align-items-flex-start">
                            <select
                              class="form-select multiselect" multiple="multiple"
                              id="add_sub_code_id" style="width:100%" disabled>

                              <option value="0">Select code</option>
                              <option
                                v-for="catcode in addicdcatcodelist"
                                v-bind:key="catcode.id"
                                v-bind:value="catcode.id">
                                {{ catcode.icd_code }}{{catcode.icd_name}}
                              </option>
                            </select>
                          </div>
                          </div>
                          </div>

                         
                          
                        </div>
                      </div>
                        <!-- 02 -->
                        <div class="external services hide mb-3">
                          <div class="row">
                            <div class="col-md-6 mb-3">
                              <label class="form-label">Services<small style="color:red">*</small> </label>
                              <select class="form-select" v-model="serviceid" disabled>
                                <option value="0">Select Service</option>
                      <option
                        v-for="slt in externallist"
                        v-bind:key="slt.id"
                        v-bind:value="slt.id"
                      >
                        {{ slt.section_value }}
                      </option>
                              </select>
                            </div>
                          </div>
                        </div>
                        <!-- 03 -->
                        <!-- hide-div -->
                        <div class="row">
                          <div class="col-md-6 mb-3">
                            <label class="form-label"
                              >Complexity Of Service<small style="color:red">*</small> </label
                            >
                            <select
                              class="form-select"
                              v-model="complexity_services" disabled
                            >
                              <option value="0">
                                Select Complexity Of Service
                              </option>
                      <option
                        v-for="cm in comlexcitylist"
                        v-bind:key="cm.id"
                        v-bind:value="cm.id"
                      >
                        {{ cm.section_value }}
                      </option>
                            </select>
                          </div>
                          <div class="col-md-6 mb-3">
                            <label class="form-label">Outcome<small style="color:red">*</small> </label>
                            <select class="form-select" v-model="outcome" disabled>
                              <option value="0">Select outcome</option>
                      <option
                        v-for="out in outcomelist"
                        v-bind:key="out.id"
                        v-bind:value="out.id"
                      >
                        {{ out.section_value }}
                      </option>
                            </select>
                          </div>
                        </div>
                        <!-- close-row -->
                      </div>
                    </div>
                  </div>
                  <!--  -->
                  <div class="accordion-item">
                    <h2 class="accordion-header" id="headingTwo">
                      <button
                        class="accordion-button collapsed"
                        type="button"
                        data-bs-toggle="collapse"
                        data-bs-target="#collapseTwo"
                        aria-expanded="false"
                        aria-controls="collapseTwo"
                      >
                        MEDICATION
                      </button>
                    </h2>
                    <div
                      id="collapseTwo"
                      class="accordion-collapse collapse"
                      aria-labelledby="headingTwo"
                      data-bs-parent="#accordionExample"
                    >
                      <div class="accordion-body">
                        <div class="col-md-12 mb-3">
                          <label class="form-label">Medication</label>
                          <textarea
                            class="form-control textarea"
                            placeholder="Please Type Prescription Here"
                            v-model="medication_des" disabled
                          ></textarea>
                        </div>
                      </div>
                    </div>
                  </div>
                  <!--  -->
                </div>

                <h4 class="sub-title form-heading">Verification</h4>
                <div class="row">
                  <div class="col-sm-6">
                    <div class="mb-3">
                      <label class="form-label">Specialist Name<small style="color:red">*</small> </label>
                      <input type="text" class="form-control" v-model="specialist_name"  disabled/>
                    </div>
                  </div>
                  <div class="col-sm-6">
                    <div class="mb-3">
                      <label class="form-label">Case Manager/Staff Name<small style="color:red">*</small> </label>
                      <input type="text" class="form-control" v-model="case_manager" disabled />
                    </div>
                  </div>
                </div>
                <!-- close-row -->
                <div class="row">
                  <div class="col-sm-6">
                    <div class="mb-3">
                      <label class="form-label">Date<small style="color:red">*</small> </label>
                      <input type="date" class="form-control" v-model="verification_date_1" disabled />
                    </div>
                  </div>
                  <div class="col-sm-6">
                    <div class="mb-3">
                      <label class="form-label">Date<small style="color:red">*</small> </label>
                      <input type="date" class="form-control" v-model="verification_date_2" disabled />
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
                <!-- close-row -->
                <br>
                <br>
                <div class="d-flex">
                    <button
                      @click="GoBack"
                      class="btn btn-primary btn-text"
                      ><i class="fa fa-arrow-alt-to-left"></i> Back
                    </button>
                   
                </div>
              </div>
            </div>
          </div>
        </div>
      </main>
      <footer>
        <p>© MENTARI MALAYSIA MOH</p>
      </footer>
    </div>
  </div>
</template>
<script>
import CommonHeader from '../../../components/CommonHeader.vue';
import CommonSidebar from '../../../components/CommonSidebar.vue';
export default {
  components: { CommonSidebar, CommonHeader },
  name: "rehab-discharge",
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    this.SidebarAccess = JSON.parse(localStorage.getItem("SidebarAccess"));
    $(document).ready(function () {
      $('.form-accordion input[type="radio"]').click(function () {
        var inputValue = $(this).attr("value");
        var targetBox = $("." + inputValue);
        $(".services").not(targetBox).hide();
        $(targetBox).show();
      });
    });
    let urlParams = new URLSearchParams(window.location.search);
    this.Id = urlParams.get("id");
    this.appId = urlParams.get("appId");
    this.GetPatientdetails();

    let urlParams1 = new URLSearchParams(window.location.search);
    this.pid = urlParams1.get("pid");
    this.type = urlParams1.get("type");

    this.GetList();
    if (this.Id) {
      this.staff_name=this.userdetails.user.name;
    }

    if (this.pid) {
      this.getdetails();
    }
  },
  mounted(){
    $(document).ready(function () {
      $(".multiselect").select2({
        placeholder: "Please Select",
      });
    });
  },
  data() {
    return {
      patientdetails: null,
      userdetails: null,
      errorList: [],
      servicelist: [],
      outcomelist: [],
      comlexcitylist: [],
      codelist: [],
      icdcatcodelist: [],
      diagonisislist: [],
      locationlist: [],
      dischargelist: [],
      Id: 0,
      name: null,
      mrn: null,
      date: null,
      time: null,
      staff_name: null,
      diagnosis_id: null,
      intervention: null,
      discharge_category: null,
      comment: null,
      location_services: 0,
      type_diagnosis_id: 0,
      category_services: null,
      code_id: 0,
      sub_code_id: 0,
      complexity_services: 0,
      outcome: 0,
      medication_des: "None.",
      patient_mrn_id: null,
      services_id: 0,
      serviceid: 0,
      validate: true,
      specialist_name: null,
      case_manager: null,
      verification_date_1: null,
      verification_date_2: null,
      assistancelist: [],
      externallist: [],
      pid:0,
      type:"",
      appId: 0,
      SidebarAccess:null,

      addicdcatcodelist: [],
      add_code_id:0,
      additional_diagnosis: [],
      additional_sub_code_id:[],
      additional_sub_code_id2:[],
    };
  },
  methods: {
   
    async GetList() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.get(
        "general-setting/list?section=" + "complexity-of-service",
        { headers }
      );
      if (response.data.code == 200 || response.data.code == "200") {
        this.comlexcitylist = response.data.list;
      } else {
        this.comlexcitylist = [];
      }
      const response1 = await this.$axios.get("service/list", { headers });
      if (response1.data.code == 200 || response1.data.code == "200") {
        this.servicelist = response1.data.list;
      } else {
        this.servicelist = [];
      }
      const response2 = await this.$axios.get(
        "general-setting/list?section=" + "outcome",
        { headers }
      );
      if (response2.data.code == 200 || response2.data.code == "200") {
        this.outcomelist = response2.data.list;
      } else {
        this.outcomelist = [];
      }
      const response3 = await this.$axios.get("diagnosis/getIcd9codeList", {
        headers,
      });
      if (response3.data.code == 200 || response3.data.code == "200") {
        this.codelist = response3.data.list;
      } else {
        this.codelist = [];
      }
      const response4 = await this.$axios.get("diagnosis/getIcd10codeList", {
        headers,
      });
      if (response4.data.code == 200 || response4.data.code == "200") {
        this.diagonisislist = response4.data.list;
      } else {
        this.diagonisislist = [];
      }
      const response5 = await this.$axios.get(
        "general-setting/list?section=" + "location-of-services",
        {
          headers,
        }
      );
      if (response5.data.code == 200 || response5.data.code == "200") {
        this.locationlist = response5.data.list;
      } else {
        this.locationlist = [];
      }
      const response6 = await this.$axios.get(
        "intervention/category-discharge",
        {
          headers,
        }
      );
      if (response6.data.code == 200 || response6.data.code == "200") {
        this.dischargelist = response6.data.list;
      } else {
        this.dischargelist = [];
      }
      const response7 = await this.$axios.get("staff-management/getList", {
        headers,
      });
      if (response7.data.code == 200 || response7.data.code == "200") {
        this.specialistlist = response7.data.list;
      } else {
        this.specialistlist = [];
      }
      const respons = await this.$axios.get(
        "general-setting/list?section=" + "assistance-or-supervision",
        { headers }
      );
      if (respons.data.code == 200 || respons.data.code == "200") {
        this.assistancelist = respons.data.list;
      } else {
        this.assistancelist = [];
      }
      const respon = await this.$axios.get(
        "general-setting/list?section=" + "external",
        { headers }
      );
      if (respon.data.code == 200 || respon.data.code == "200") {
        this.externallist = respon.data.list;
      } else {
        this.externallist = [];
      }
    },
    async onCategorycodebind(event) {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      console.log("my id", event);
      const response = await this.$axios.post(
        "diagnosis/getIcd9subcodeList",
        { icd_category_code: event.target.value },
        { headers }
      );
      if (response.data.code == 200 || response.data.code == "200") {
        this.icdcatcodelist = response.data.list;
      } else {
        this.icdcatcodelist = [];
      }
    },
     async GetPatientdetails() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "patient-registration/getPatientRegistrationById",
        {
          id: this.Id,
        },
        { headers }
      );
      if (response.data.code == 200 || response.data.code == "200") {
        this.mrn= response.data.list[0].patient_mrn;
        this.name= response.data.list[0].name_asin_nric;
        console.log("my details", this.patientdetails);
      } else {
        this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + this.error,
                  footer: ''
                });
      }
    },
    async resetmodel() {
      this.name = "";
      this.mrn = "";
      this.date = "";
      this.time = "";
      this.staff_name = "";
      this.diagnosis_id = "";
      this.intervention = "";
      this.discharge_category = "";
      this.comment = "";
      this.specialist_name = "";
      this.case_manager = "";
      this.verification_date_1 = "";
      this.verification_date_2 = "";
      this.location_services = 0;
      this.services_id = 0;
      this.code_id = 0;
      this.sub_code_id = 0;
      this.type_diagnosis_id = 0;
      this.category_services = 0;
      this.complexity_services = 0;
      this.outcome = 0;
      this.medication_des = "";
    },
     async getdetails() {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "/patient-appointment-details/fetchViewHistoryListDetails",
        {
          id: this.pid,
          type: "RehabDischargeNote",
        },
        { headers }
      );
      if (response.data.code == 200 || response.data.code == "200") {
        // window.alert(response.data.Data[0].patient_mrn_id);


        this.name = response.data.Data[0].name;
        this.time = response.data.Data[0].time;
        this.comment = response.data.Data[0].comment;
        this.mrn = response.data.Data[0].mrn;
        this.date = response.data.Data[0].date;
        this.staff_name = response.data.Data[0].staff_name;
        this.diagnosis_id = response.data.Data[0].diagnosis_id;
        if (response.data.Data[0].intervention == "supportedEmployment"){
          this.intervention = "supportedEmployment"
        }else if (response.data.Data[0].intervention == "ETP"){
          this.intervention = "ETP"
        }else if (response.data.Data[0].intervention == "jobClub"){
          this.intervention = "jobClub"
        }
        this.discharge_category = response.data.Data[0].discharge_category;
        this.location_services = response.data.Data[0].location_services;
        this.type_diagnosis_id = response.data.Data[0].diagnosis_type;
        this.category_services = response.data.Data[0].service_category;
        this.code_id = response.data.Data[0].code_id;
        this.sub_code_id = response.data.Data[0].sub_code_id;
        this.complexity_services =
          response.data.Data[0].complexity_services;
        this.outcome = response.data.Data[0].outcome;
        this.medication_des = response.data.Data[0].medication;
        this.services_id = response.data.Data[0].services_id;
        this.specialist_name = response.data.Data[0].specialist_name;
        this.verification_date_1 = response.data.Data[0].verification_date_1;
        this.verification_date_2 = response.data.Data[0].verification_date_2;
        this.case_manager = response.data.Data[0].case_manager;
        this.GetList();
        this.GetPatientdetails();
        const response2 = await this.$axios.post(
          "diagnosis/getIcd9subcodeList",
          { icd_category_code: this.code_id },
          { headers }
        );
        if (response2.data.code == 200 || response2.data.code == "200") {
          this.icdcatcodelist = response2.data.list;

        } else {
          this.icdcatcodelist = [];
        }

      } else {
        this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + this.error,
                  footer: ''
                });
      }
    },

    async onCategoryaddcodebind(event) {
      const headers = {
        Authorization: "Bearer " + this.userdetails.access_token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "diagnosis/getIcd9subcodeList",
        { icd_category_code: event.target.value },
        { headers }
      );
      if (response.data.code == 200 || response.data.code == "200") {
        this.addicdcatcodelist = response.data.list;
      } else {
        this.addicdcatcodelist = [];
      }
    },
    async GoBack(){
      if (this.type == 'view'){
        this.$router.go(-1);
      } else {
        this.$router.push({
              path: "/modules/Intervention/patient-summary",
              query: { id: this.Id, appId: this.appId },
            });
      }
    }
  },
};
</script>

<style scoped>
.hide {
  display: none;
}
</style>
