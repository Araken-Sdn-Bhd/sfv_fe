<template>
  <div>
    <table class="notes">
      <thead>
        <tr>
          <th colspan="2">STAFF DETAILS</th>
        </tr>
      </thead>
      <tbody v-if="userdetails">
        <tr>
          <th>Staff Name / Seen By:</th>
          <td>{{ userdetails.user.name }}</td>
        </tr>
        <tr>
          <th>Designation:</th>
          <td>{{ userdetails.user.role }}</td>
        </tr>
        <!-- <tr>
          <th>Room:</th>
          <td>-</td>
        </tr> -->
        <tr>
          <th>Date:</th>
          <td>{{ currentdate }}</td>
        </tr>
        <tr>
          <th>Time:</th>
          <td>{{ currenttime }}</td>
        </tr>
      </tbody>
    </table>
    <table class="notes" v-if="patientdetails">
      <thead>
        <tr>
          <th colspan="2">Patient Details</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th>MRN:</th>
          <td>{{ patientdetails.patient_mrn }}</td>
        </tr>
        <tr>
          <th>Patient Name:</th>
          <td>{{ patientdetails.name_asin_nric }}</td>
        </tr>
        <tr>
          <th>NRIC NO:</th>
          <td>{{ patientdetails.nric_no }}</td>
        </tr>
        <tr>
          <th>Age:</th>
          <td>{{ patientdetails.age }}</td>
        </tr>
        <tr>
          <th>Contact No:</th>
          <td>{{ patientdetails.mobile_no }}</td>
        </tr>
        <tr>
          <th>Gender:</th>
          <td>{{ patientdetails.gender[0].section_value }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      userdetails: null,
      Id: 0,
      patientdetails: null,
    };
  },
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    let urlParams = new URLSearchParams(window.location.search);
    this.Id = urlParams.get("id");
    this.GetPatientdetails();
    const current = new Date();
    this.currentdate =
      current.getDate() +
      "-" +
      (current.getMonth() + 1) +
      "-" +
      current.getFullYear();

    this.currenttime = current.getHours() + ":" + current.getMinutes();
  },
  methods: {
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
      if (response.data.code == 200) {
        this.patientdetails = response.data.list[0];
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
  },
};
</script>
