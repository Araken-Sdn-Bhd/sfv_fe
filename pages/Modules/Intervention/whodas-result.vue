<template>
  <div id="layoutSidenav">
    <CommonSidebar />

    <div id="layoutSidenav_content">
      <CommonHeader />

      <main>
        <div class="container-fluid px-4">
          <nav class="offline-form" v-if="!userdetails">
            <ul>
              <li>
                <a href="/app/modules/Patient/cbi" class="nav-link"
                  ><i class="fa fa-file-contract"></i> <span>CBI</span></a
                >
              </li>
              <li>
                <a href="/app/modules/Patient/dass" class="nav-link"
                  ><i class="fa fa-file-contract"></i> <span>DASS</span></a
                >
              </li>
              <li>
                <a href="/app/modules/Patient/phq-9" class="nav-link"
                  ><i class="fa fa-file-contract"></i> <span>PHQ 9</span></a
                >
              </li>
              <li>
                <a href="/app/modules/Patient/whodas" class="nav-link"
                  ><i class="fa fa-file-contract"></i> <span>WHODAS</span></a
                >
              </li>
            </ul>
          </nav>
          <div :class="userdetails ? 'page-title' : 'offline-title'">
            <h1>Patient Screening and Appointment</h1>
          </div>
          <div class="card mb-4">
            <div
              class="result"
              id="results"
              style="background: #fff !important"
            >
              <div class="result-header">
                <h4>Who Disabilty Assessment schedule (WHO DAS)</h4>
                <p>Thank you for reaching out to MENTARI Self Test</p>
              </div>
              <div class="row justify-content-center">
                <div class="col-sm-8">
                  <div class="whodas-result">
                    <p>Your general disability score</p>
                    <h4>{{ UserTotal }} <span>/ 180</span></h4>
                  </div>

                  <div class="row">
                    <div class="col-sm-6">
                      <div class="whodas-box">
                        <h5>UNDERSTANDING & COMMUNICATING</h5>
                        <div class="score-box">
                          <h4>{{ UC }}</h4>
                          <span>Domain Score</span>
                        </div>
                      </div>
                    </div>
                    <!-- col-sm-6 -->

                    <div class="col-sm-6">
                      <div class="whodas-box">
                        <h5>GETTING AROUND</h5>
                        <div class="score-box">
                          <h4>{{ GA }}</h4>
                          <span>Domain Score</span>
                        </div>
                      </div>
                    </div>
                    <!-- col-sm-6 -->

                    <div class="col-sm-6">
                      <div class="whodas-box">
                        <h5>SELF CARE</h5>
                        <div class="score-box">
                          <h4>{{ SC }}</h4>
                          <span>Domain Score</span>
                        </div>
                      </div>
                    </div>
                    <!-- col-sm-6 -->

                    <div class="col-sm-6">
                      <div class="whodas-box">
                        <h5>GETTING ALONG WITH PEOPLE</h5>
                        <div class="score-box">
                          <h4>{{ GAWP }}</h4>
                          <span>Domain Score</span>
                        </div>
                      </div>
                    </div>
                    <!-- col-sm-6 -->

                    <div class="col-sm-6">
                      <div class="whodas-box">
                        <h5>LIFE ACTIVITIES - HOUSEHOLD</h5>
                        <div class="score-box">
                          <h4>{{ LAH }}</h4>
                          <span>Domain Score</span>
                        </div>
                      </div>
                    </div>
                    <!-- col-sm-6 -->

                    <div class="col-sm-6">
                      <div class="whodas-box">
                        <h5>LIFE ACTIVITIES - SCHOOL/WORK</h5>
                        <div class="score-box">
                          <h4>{{ LASW }}</h4>
                          <span>Domain Score</span>
                        </div>
                      </div>
                    </div>
                    <!-- col-sm-6 -->

                    <div class="col-sm-6">
                      <div class="whodas-box">
                        <h5>PARTICIPATION IN SOCIETY</h5>
                        <div class="score-box">
                          <h4>{{ PIS }}</h4>
                          <span>Domain Score</span>
                        </div>
                      </div>
                    </div>
                    <!-- col-sm-6 -->
                  </div>
                </div>
              </div>
            </div>
            <div class="row justify-content-center">
              <div class="col-sm-8">
                <div class="d-flex mt-3">
                  <a
                      @click="GoBack"
                      class="btn btn-primary btn-text"
                      ><i class="fa fa-arrow-alt-to-left"></i> Back</a
                    >

                </div>
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
  name: "dass-result",
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
        src: "https://cdnjs.cloudflare.com/ajax/libs/jspdf/1.3.2/jspdf.min.js",
        async: true,
        crossorigin: "anonymous",
      },
    ],
  },
  data() {
    return {
      userdetails: null,
      whodasresult: null,
      GA: 0,
      GAWP: 0,
      LAH: 0,
      LASW: 0,
      PIS: 0,
      SC: 0,
      UC: 0,
      GAlevel: "",
      GAWPlevel: "",
      LAHlevel: "",
      LASWlevel: "",
      PISlevel: "",
      SClevel: "",
      UClevel: "",
      UserTotal: 0,
      Id:0,
      appId: 0,
    };
  },
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    this.whodasresult = JSON.parse(localStorage.getItem("whodasresult"));
    console.log("my res", this.whodasresult);
    if (this.whodasresult) {
      this.GA = this.whodasresult.GA.score;
      this.GAWP = this.whodasresult.GAWP.score;
      this.LAH = this.whodasresult.LAH.score;
      this.LASW = this.whodasresult.LASW.score;
      this.PIS = this.whodasresult.PIS.score;
      this.SC = this.whodasresult.SC.score;
      this.UC = this.whodasresult.UC.score;
      this.GAlevel = this.whodasresult.GA.level;
      this.GAWPlevel = this.whodasresult.GAWP.level;
      this.LAHlevel = this.whodasresult.LAH.level;
      this.LASWlevel = this.whodasresult.LASW.level;
      this.PISlevel = this.whodasresult.PIS.level;
      this.SClevel = this.whodasresult.SC.level;
      this.UClevel = this.whodasresult.UC.level;
      this.UserTotal = this.whodasresult.UserTotal;
    }
     let urlParams = new URLSearchParams(window.location.search);
     let urlParams2 = new URLSearchParams(window.location.search);

       this.Id = urlParams.get("id");
       this.appId = urlParams2.get("appId");
  },
  beforeDestroy() {
    localStorage.removeItem("whodasresult");
  },
  methods: {
    demoFromHTML() {
      var pdf = new jsPDF("p", "pt", "a4");
      pdf.addHTML($("#results")[0], function () {
        pdf.save("Result.pdf");
      });
    },
    GoBack(){
      this.$router.push({
              path: "/modules/Intervention/patient-summary",
              query: { id: this.Id, appId: this.appId },
            });
    }
  },
};
</script>
