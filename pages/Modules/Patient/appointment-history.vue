<template>
  <div id="layoutSidenav">
    <CommonSidebar />
    <div id="layoutSidenav_content">
      <CommonHeader />
      <main>
        <div class="container-fluid px-4">
          <PatientDetails />
          <!-- card -->
          <div class="card mb-4">
            <div class="card-header">
              <h4>Appointment History Record</h4>
            </div>
            <div class="card-body">
              <table class="table table-striped data-table" style="width: 100%">
                <thead>
                  <tr>
                    <th>No</th>
                    <th>Date</th>
                    <th>Time</th>
                    <th>Status</th>
                    <th width="100px">Action</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(app, index) in list" :key="index">
                    <td>{{ index+1 }}</td>
                    <td>{{ app.booking_date }}</td>
                    <td>{{ app.booking_time }}</td>
                    <td>
                      <span
                        v-if="app.appointment_status == 3"
                        class="badge bg-primary"
                        >Completed</span
                      >
                      <span
                        v-if="app.appointment_status == 4"
                        class="badge bg-success"
                        >Ready</span
                      >
                      <span
                        v-if="app.appointment_status == 1"
                        class="badge bg-warning text-dark"
                        >Processing</span
                      >
                      <span
                        v-if="app.appointment_status == 2"
                        class="badge bg-danger"
                        >No Show</span
                      >
                    </td>

                    <td>
                      <a
                        @click="oneditAppointment(app.id)"
                        style="cursor: pointer"
                        class="edit"
                        ><i class="fa fa-edit"></i
                      ></a>
                    </td>
                  </tr>
                  <tr style="display: none">
                    <td>2</td>
                    <td>5/6/2021</td>
                    <td>11:00AM</td>
                    <td>No Show</td>
                    <td>
                      <a href="#" class="edit"><i class="fa fa-edit"></i></a>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
          <!-- card -->
        </div>
      </main>
    </div>
  </div>
</template>
<script>
import PatientDetails from "../../../components/Patient/PatientDetails.vue";
import CommonHeader from '../../../components/CommonHeader.vue';
import CommonSidebar from '../../../components/CommonSidebar.vue';
export default {
  components: { CommonSidebar, CommonHeader, PatientDetails },
  name: "patient-summary",
  data() {
    return {
      userdetails: null,
      errorList: [],
      list: [],
      Id: 0,
    };
  },
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    let urlParams = new URLSearchParams(window.location.search);
    this.Id = urlParams.get("id");
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
        `${this.$axios.defaults.baseURL}`+"patient-appointment-details/getPatientAppointmentDetailsOfPatient",
        { patient_id: this.Id },
        { headers }
      )
      .then((resp) => {
        this.list = resp.data.list;
        $(document).ready(function () {
          $(".data-table").DataTable({
            searching: false,
            bLengthChange: false,
            bInfo: false,
            autoWidth: false,
            responsive: true,
            language: {
              paginate: {
                next: '<i class="fad fa-arrow-to-right"></i>', // or '→'
                previous: '<i class="fad fa-arrow-to-left"></i>', // or '←'
              },
            },
          });
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
    oneditAppointment(Id) {
      this.$router.push({
        path: "/modules/Patient/book-appointment",
        query: { id: Id },
      });
    },
  },
};
</script>
