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
                        <h5>LIFE ACTIVMES - SCHOOL/WORK</h5>
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
      appId: 0
    };
  },
  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    this.whodasresult = JSON.parse(localStorage.getItem("whodasresult_history"));
    console.log("my res", this.whodasresult);
    if (this.whodasresult) {
      const Array=this.whodasresult.test_section_name.split(',');
      console.log("my res", Array);
      const Results=this.whodasresult.results.split(',');
      console.log("my result", Results);
      if(Array[0] =="UC"){
        this.UC = Results[0];
      } if(Array[1] =="GA"){
        this.GA = Results[1];
      }
       if(Array[2] =="SC"){
        this.SC = Results[2];
      }
      if(Array[3] =="GAWP"){
        this.GAWP = Results[3];
      }
       if(Array[4] =="LAH"){
        this.LAH = Results[4];
      }
       if(Array[5] =="LASW"){
        this.LASW = Results[5];
      }
      if(Array[6] =="PIS"){
        this.PIS = Results[6];
      }
      this.UserTotal = this.whodasresult.result;
    }
     let urlParams = new URLSearchParams(window.location.search);
       this.Id = urlParams.get("id");
    
     let urlParams1 = new URLSearchParams(window.location.search);
       this.appId = urlParams1.get("appId");
  },
  beforeDestroy() {
    localStorage.removeItem("whodasresult");
  },
  methods: {
    GoBack(){
      if(this.appId){
        this.$router.push({
              path: "/modules/Intervention/patient-summary",
              query: { id: this.Id, appId: this.appId },
            });
      }else{
        this.$router.push({
              path: "/modules/Intervention/patient-summary",
              query: { id: this.Id},
            });
      };
    },
    demoFromHTML() {
      var pdf = new jsPDF("p", "pt", "a4");
      pdf.addHTML($("#results")[0], function () {
        pdf.save("Result.pdf");
      });
    },
    async Gotorequestappointment() {
      this.$router.push({
        path: "/modules/Intervention/request-appointment-form",
        query: { id: this.Id },
      });
    }
  },
};
</script>
