<template>
  <div id="layoutSidenav">
    <div id="layoutSidenav_nav">
      <nav class="sb-sidenav accordion sb-sidenav-dark" id="sidenavAccordion">
        <div class="sb-sidenav-menu scrool">
          <div class="nav">
            <ul>
              <li>
                <a class="nav-link" href="#">
                  <i class="fa fa-home-alt"></i>
                  <span>Dashboard</span>
                </a>
              </li>

              <li class="sub-menu">
                <a
                  class="nav-link collapsed"
                  href="#"
                  data-bs-toggle="collapse"
                  data-bs-target="#system-setting"
                  aria-expanded="true"
                  aria-controls="system-setting"
                >
                  <i class="fa fa-file-chart-line"></i>
                  Workload Report
                </a>
                <ul
                  class="collapse"
                  id="system-setting"
                  aria-labelledby="headingOne"
                  data-bs-parent="#sidenavAccordion"
                >
                  <li class="">
                    <a class="nav-link" href="/app/modules/Report/general-report">
                      <i class="fa fa-file-chart-pie"></i>
                      <span>General Report</span>
                    </a>
                  </li>
                  <li>
                    <a
                      class="nav-link"
                      href="/app/modules/Report/total-patient-and-type-of-referral"
                    >
                      <i class="fa fa-file-chart-pie"></i>
                      <span>Total Patient & Type Of Referral</span>
                    </a>
                  </li>
                  <li>
                    <a
                      class="nav-link"
                      href="/app/modules/Report/patient-by-age-gender-and-ethnic-group"
                    >
                      <i class="fa fa-file-chart-pie"></i>
                      <span>Patient By Age/gender & Ethnic Group</span>
                    </a>
                  </li>
                  <li>
                    <a class="nav-link" href="/app/modules/Report/request-appointment-report">
                      <i class="fa fa-file-chart-pie"></i>
                      <span>Request Appointment Report</span>
                    </a>
                  </li>
                </ul>
              </li>
              <!-- sub-menuc -->

              <li class="sub-menu">
                <a
                  class="nav-link collapsed"
                  href="#"
                  data-bs-toggle="collapse"
                  data-bs-target="#activities-report"
                  aria-expanded="true"
                  aria-controls="activities-report"
                >
                  <i class="fa fa-file-chart-line"></i>
                  <span>Activities Report</span>
                </a>
                <ul
                  class="collapse"
                  id="activities-report"
                  aria-labelledby="headingOne"
                  data-bs-parent="#sidenavAccordion"
                >
                  <li>
                    <a class="nav-link" href="/app/modules/Report/activities-report-patient">
                      <i class="fa fa-file-chart-pie"></i>
                      <span>Patient</span>
                    </a>
                  </li>
                  <li>
                    <a class="nav-link" href="/app/modules/Report/activities-report-VON">
                      <i class="fa fa-file-chart-pie"></i>
                      <span>VON</span>
                    </a>
                  </li>
                </ul>
              </li>
              <!-- sub-menuc -->

              <li>
                <a class="nav-link" href="/app/modules/Report/national-kpi">
                  <i class="fa fa-file-chart-line"></i>
                  <span>National KPI</span>
                </a>
              </li>

              <li class="active">
                <a class="nav-link" href="/app/modules/Report/sharp">
                  <i class="fa fa-file-chart-line"></i>
                  <span>SHHARP</span>
                </a>
              </li>
              <li class="divider">Imported Link</li>
              <div>
                <li>
                  <a href="/app/modules/Patient/patient-list" class="nav-link">
                    <i class="fa fa-home-alt"></i>
                    Patient Manag...
                  </a>
                </li>

                <li>
                  <a href="/app/modules/Admin/admin-dashboard" class="nav-link">
                    <i class="fa fa-home-alt"></i>
                    Admin Manag...
                  </a>
                </li>

                <li>
                  <a href="/app/modules/Intervention/patient-list" class="nav-link">
                    <i class="fa fa-home-alt"></i>
                    Intervention Manag...
                  </a>
                </li>
                <li>
                  <a href="/app/modules/Shharp/patients-list" class="nav-link">
                    <i class="fa fa-home-alt"></i>
                    Shharp Manag...
                  </a>
                </li>
              </div>
            </ul>
          </div>
        </div>
      </nav>
    </div>
    <div
      class="modal fade"
      id="insertpopup"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered modal-sm test-connection">
        <div class="modal-content">
          <div class="modal-body">
            <p>Successfully Created</p>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary btn-ok"
              data-bs-dismiss="modal"
            >
              Ok
            </button>
          </div>
        </div>
      </div>
    </div>
    <div
      class="modal fade"
      id="updatepopup"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered modal-sm test-connection">
        <div class="modal-content">
          <div class="modal-body">
            <p>Successfully Updated</p>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary btn-ok"
              data-bs-dismiss="modal"
            >
              Ok
            </button>
          </div>
        </div>
      </div>
    </div>
    <div
      class="modal fade"
      id="errorpopup"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered modal-sm test-connection">
        <div class="modal-content">
          <div class="modal-body">
            <p>Something went wrong!</p>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary btn-ok"
              data-bs-dismiss="modal"
            >
              Ok
            </button>
          </div>
        </div>
      </div>
    </div>
    <div
      class="modal fade"
      id="deletepopup"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered modal-sm test-connection">
        <div class="modal-content">
          <div class="modal-body">
            <p>Succesfully Deleted</p>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary btn-ok"
              data-bs-dismiss="modal"
            >
              Ok
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "ReportSidebar",
  head: {
    script: [
      {
        src: "/app/js/bootstrap.bundle.min.js",
        body: true,
        crossorigin: "anonymous",
      },

      {
        src: "/app/js/jquery-3.5.1.js",
        body: true,
        crossorigin: "anonymous",
      },
      {
        src: "/app/js/scripts.js",
        body: true,
        crossorigin: "anonymous",
      },
      {
        src: "/app/js/jquery.dataTables.min.js",
        body: true,
        crossorigin: "anonymous",
      },
      {
        src: "/app/js/dataTables.bootstrap5.min.js",
        body: true,
        crossorigin: "anonymous",
      },
      {
        src: "https://cdn.jsdelivr.net/npm/select2@4.1.0-rc.0/dist/js/select2.min.js",
        body: true,
        crossorigin: "anonymous",
      },
      {
        src: "https://cdnjs.cloudflare.com/ajax/libs/jspdf/1.3.2/jspdf.min.js",
        async: true,
        crossorigin: "anonymous",
      },
    ],
  },
  data() {
    return {
      userdetails: null,
      nav: "",
    };
  },
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    if (!this.userdetails) {
      this.$router.push("/");
    }
  },
  mounted() {
     document.body.classList.add("sb-nav-fixed");
 
  },
  methods: {
 
  },
};
</script>
