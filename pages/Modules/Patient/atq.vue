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
              <h4>AUTOMATIC THOUGHT QUESTIONARE (ATQ)</h4>
            </div>
            <div class="card-body">
              <div class="form-title mt-2">
                <p>
                  [1 - Not at All; 2 - Sometimes; 3- Moderately Often; 4- Often
                  and 5- All the time]
                </p>
              </div>

              <table class="form-table">
                <thead>
                  <tr>
                    <th width="50%"></th>
                    <th width="50%"></th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(atq, index) in list" :key="index">
                    <td>{{ atq.Question }}</td>
                    <td>
                      <div class="form-check form-check-inline">
                        <input
                          class="form-check-input"
                          type="radio"
                          v-bind:name="'atq' + index"
                          value="1"
                          @change="onchange(atq.id, 1)"
                        />
                        <label class="form-check-label" for="1">1</label>
                      </div>
                      <div class="form-check form-check-inline">
                        <input
                          class="form-check-input"
                          type="radio"
                          v-bind:name="'atq' + index"
                          value="2"
                          @change="onchange(atq.id, 2)"
                        />
                        <label class="form-check-label" for="2">2</label>
                      </div>
                      <div class="form-check form-check-inline">
                        <input
                          class="form-check-input"
                          type="radio"
                          v-bind:name="'atq' + index"
                          value="3"
                          @change="onchange(atq.id, 3)"
                        />
                        <label class="form-check-label" for="3">3</label>
                      </div>
                      <div class="form-check form-check-inline">
                        <input
                          class="form-check-input"
                          type="radio"
                          v-bind:name="'atq' + index"
                          value="4"
                          @change="onchange(atq.id, 4)"
                        />
                        <label class="form-check-label" for="4">4</label>
                      </div>
                      <div class="form-check form-check-inline">
                        <input
                          class="form-check-input"
                          type="radio"
                          v-bind:name="'atq' + index"
                          value="5"
                          @change="onchange(atq.id, 5)"
                        />
                        <label class="form-check-label" for="5">5</label>
                      </div>
                    </td>
                  </tr>
                </tbody>
              </table>
              <Error :message="error" v-if="error" />
              <div class="d-flex align-items-center mt-2">
                <button
                  type="submit"
                  class="btn btn-success ml-auto"
                @click="OnsubmitTest"
                >
                  <i class="fad fa-paper-plane"></i> Submit
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
                  <h5 class="modal-title">ATQ Alert</h5>
                  <p>
                    Your Test is successfully Submitted!
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
                        <th scope="row">{{result.ATQ}}</th>
                        <td>{{result.atqScore}}</td>
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
  name: "bai",
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
        { Type: "atq" },
        { headers }
      );
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
              test_name: "atq",
              test_section_name: "ATQ",
              result: JSON.stringify([{ ATQ: this.checkedList }]),
              user_ip_address: this.Ipaddress,
            },
            { headers }
          );
          if (response.data.code == 200 || response.data.code == "200") {
            this.loader = false;
            this.result = response.data.result;
            this.$nextTick(() => {
              $("#resultmodal").modal("show");
            });
            this.$router.push({
              path: "/modules/Intervention/patient-summary",
              query: { id: this.Id },
            });
          } else {
            this.loader = false;
            this.$swal.fire({
                  icon: 'error',
                  title: 'Oops... Something Went Wrong!',
                  text: 'the error is: ' + JSON.stringify(response.data.message),
                  footer: ''
                });
          }
        } else {
          this.error = "Please attempt all question";
        }
      } catch (e) {
        this.loader = false;
        this.errors = e;
        console;
      }
    },
    downloadresult() {
      var pdf = new jsPDF("p", "pt", "a4");
      pdf.addHTML($("#results")[0], function () {
        pdf.save("Result.pdf");
      });
    },
      async Gotorequestappointment() {
      this.$router.push({
        path: "/modules/Patient/request-appointment-form",
        query: { id: this.Id },
      });
    },
  },
};
</script>
