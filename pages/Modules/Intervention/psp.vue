<template>
  <div id="layoutSidenav">
    <CommonSidebar />
    <div id="layoutSidenav_content">
      <CommonHeader />
      <main>
        <Loader v-if="loader" />
        <div class="container-fluid px-4">
          <div class="page-title">
            <h1>Patient Screening and Appointment</h1>
            <!-- <a href="demographic.html"><i class="fal fa-plus"></i> Add</a> -->
          </div>

          <div class="card mb-4">
            <div class="card-header bg-transparent">
              <h4>PERSONAL AND SOCIAL PERFORMANCE SCALE (PSP)</h4>
            </div>
            <div class="card-body">
              <table class="data-info mt-3 mb-3">
                <thead>
                  <tr>
                    <th colspan="2"></th>
                    <th class="text-center">Absent</th>
                    <th class="text-center">Mild</th>
                    <th class="text-center">Manifest</th>
                    <th class="text-center">Marked</th>
                    <th class="text-center">Severe</th>
                    <th class="text-center">Very Severe</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(psp, index) in list" :key="index">
                    <th colspan="2">
                      {{ psp.Question }}
                    </th>
                    <td class="text-center">
                      <input
                        class="form-check-input"
                        type="radio"
                        v-bind:name="'psp' + index"
                        value="0"
                        @change="onchange(psp.id, 0)"
                      />
                    </td>
                    <td class="text-center">
                      <input
                        class="form-check-input"
                        type="radio"
                        v-bind:name="'psp' + index"
                        value="1"
                        @change="onchange(psp.id, 1)"
                      />
                    </td>
                    <td class="text-center">
                      <input
                        class="form-check-input"
                        type="radio"
                        v-bind:name="'psp' + index"
                        value="2"
                        @change="onchange(psp.id, 2)"
                      />
                    </td>
                    <td class="text-center">
                      <input
                        class="form-check-input"
                        type="radio"
                        v-bind:name="'psp' + index"
                        value="3"
                        @change="onchange(psp.id, 3)"
                      />
                    </td>
                    <td class="text-center">
                      <input
                        class="form-check-input"
                        type="radio"
                        v-bind:name="'psp' + index"
                        value="4"
                        @change="onchange(psp.id, 4)"
                      />
                    </td>
                    <td class="text-center">
                      <input
                        class="form-check-input"
                        type="radio"
                        v-bind:name="'psp' + index"
                        value="5"
                        @change="onchange(psp.id, 5)"
                      />
                    </td>
                  </tr>
                </tbody>
              </table>
              <Error :message="error" v-if="error" />
              <br><br>
              <div class="d-flex">
                  <button @click="GoBack" type="button" class="btn btn-primary btn-fill btn-md" title="Back">
                    <i class="fa fa-step-backward"/> &nbsp; Back
                </button>
                  <button type="submit" class="btn btn-warning btn-text ml-auto btn-fill btn-md" title="Save" @click="OnsubmitTest">
                    <i class="fa fa-save"></i> Save
                  </button>
                </div>
            </div>
          </div>
        </div>
        <div class="modal fade" id="resultmodal" tabindex="-1">
          <div class="modal-dialog modal-dialog-centered modal-table-body">
            <div class="modal-content">
              <div id="results" style="background: #fff">
                <div class="modal-header">
                   <h5 class="modal-title">PSP Alert</h5>
                  <p>
                    Your Test Successfully Submitted!
                  </p>
                </div>
                <!-- <div class="modal-body">
                  <table class="modal-table">
                    <thead>
                      <tr>
                        <th scope="col">Level</th>
                        <th scope="col">Total Scrore</th>
                      </tr>
                    </thead>
                  <tbody>
                      <tr class="active" v-if="result">
                        <th scope="row">{{result.PSP}}</th>
                        <td>{{result.pspScore}}</td>
                      </tr>
                    </tbody>
                  </table>
                </div> -->
              </div>
              <!-- <div class="modal-footer">
                <button
                  @click="downloadresult"
                  type="button"
                  class="btn btn-secondary mr-auto"
                >
                  <i class="fad fa-download"></i> Download Result
                </button>
                <a
                 @click="Gotorequestappointment"
                  class="btn btn-primary ml-auto"
                >
                  <i class="fad fa-calendar-day"></i> Request Appointment
                </a>
              </div> -->
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
  name: "psp",
  data() {
    return {
      userdetails: null,
      list: [],
      Ipaddress: "",
      checkedList: {},
      error: null,
      loader: false,
      userId: 0,
      token: "",
      Id: 0,
      result: null,
      appId: 0,
    };
  },
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    this.GetList();
    this.GetUserIpAddress();
    if (this.userdetails) {
      this.userId = this.userdetails.user.id;
      this.token = this.userdetails.access_token;
    }
    let urlParams = new URLSearchParams(window.location.search);
    this.Id = urlParams.get("id");
    let urlParams2 = new URLSearchParams(window.location.search);
    this.appId = urlParams2.get("appId");
  },
  methods: {
    async GetList() {
      const headers = {
        Authorization: "Bearer " + this.token,
        Accept: "application/json",
        "Content-Type": "application/json",
      };
      const response = await this.$axios.post(
        "patient-online-self-test/list-type",
        { Type: "psp" },
        { headers }
      );
      console.log("psp", response.data);
      if (response.data.code == 200 || response.data.code == "200") {
        this.list = response.data.list;
      } else {
        this.list = [];
      }
    },
   async GetUserIpAddress() {
      const {
        data: { ip },
      } = await this.$axios.get("https://www.cloudflare.com/cdn-cgi/trace", {
        responseType: "text",
        transformResponse: (data) =>
          Object.fromEntries(
            data
              .trim()
              .split("\n")
              .map((line) => line.split("="))
          ),
      });
      this.Ipaddress = ip;
    },
    onchange(ind, val) {
      this.checkedList[ind] = val;
    },
    async OnsubmitTest() {
      this.$swal.fire({
                title: 'Do you want to submit this entry?',
                showCancelButton: true,
                confirmButtonText: 'Save',
            }).then(async (result) => {
              if (result.isConfirmed) {
                  this.error = null;
                  try {
                    if (this.list.length == Object.values(this.checkedList).length) {
                      this.loader = true;
                      const headers = {
                        Authorization: "Bearer " + this.token,
                        Accept: "application/json",
                        "Content-Type": "application/json",
                      };
                      const response = await this.$axios.post(
                        "patient/online-test",
                        {
                          added_by: this.userId,
                          patient_id: this.Id,
                          test_name: "psp",
                          test_section_name: "PSP",
                          result: JSON.stringify([{ PSP: this.checkedList }]),
                          user_ip_address: this.Ipaddress,
                        },
                        { headers }
                      );
                      console.log("my reslut", response.data);
                      if (response.data.code == 200 || response.data.code == "200") {
                        this.loader = false;
                        this.result = response.data.result;
                        this.$router.push({
                          path: "/modules/Intervention/psychometric-history",
                          query: { id: this.Id, appId: this.appId },
                        });
                        this.$swal.fire({
                                    icon: 'success',
                                    title: 'Result is successfully submitted.',
                                    showConfirmButton: false,
                                    timer: 1500
                                    });
                      } else {
                        this.loader = false;
                        this.$swal.fire({
                                    icon: 'error',
                                    title: 'Oops... Something Went Wrong!',
                                    text: 'the error is: ' + JSON.stringify(response.data.message),
                      })
                      }
                    } else {
                      this.$swal.fire({
                                    icon: 'error',
                                    title: 'Please attempt all questions!',
                                    text: '',
                      })
                    }
                  } catch (e) {
                    this.loader = false;
                    this.$swal.fire({
                            icon: 'error',
                            title: 'Oops... Something Went Wrong!',
                            text: 'the error is: ' + e,
                        })
                  }
              } else if (result.isDismissed) {
                    this.$swal.fire('Changes are not saved', '', 'info')
              }
            })
    },
    GoBack(){
      this.$router.push({
              path: "/modules/Intervention/patient-summary",
              query: { id: this.Id, appId: this.appId },
            });
    },
    downloadresult() {
      var pdf = new jsPDF("p", "pt", "a4");
      pdf.addHTML($("#results")[0], function () {
        pdf.save("Result.pdf");
      });
    },

  },
};
</script>
