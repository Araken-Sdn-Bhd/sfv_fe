<template>
  <div id="layoutSidenav">
    <div>
      <CommonSidebar />
    </div>
    <div id="layoutSidenav_content">
      <div>
        <CommonHeader />
      </div>
      <main>
        <div class="container-fluid px-4">
          <div class="page-title">
            <h1>Calendar</h1>
            <a href="/app/modules/Patient/book-appointment" class="add-btn"
              ><i class="fal fa-plus"></i
            ></a>
          </div>
          <div class="card mb-4">
            <div class="card-body">
              <div class="search-table mt-3">
                <div class="row">
                  <div class="col-sm-5 mb-4">
                    <select class="form-select" v-model="team" @change="OnSearch()">
                      <option value="">Select Assigned Team</option>
                      <option
                        v-for="tea in teamlist"
                        v-bind:key="tea.team_name"
                        v-bind:value="tea.team_name"
                      >
                        {{ tea.team_name }}
                      </option>
                    </select>
                  </div>

                  <div class="col-sm-5 ml-auto mb-4 search-box">
                    <div class="input-group">
                      <span class="input-group-text" id="basic-addon1">
                        <i class="fa fa-search"></i>
                      </span>
                      <input
                        type="text"
                        class="form-control"
                        placeholder="Search By Name/NRIC/Passport/MRN"
                        v-model="search"
                        @keyup="OnSearch"
                      />
                    </div>
                  </div>
                </div>
              </div>
              <div class="calendar" id="calendar"></div>
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
import "@/assets/css/fullcalendar.css";
import moment from 'moment';
export default {
  components: { CommonSidebar, CommonHeader },
  name: "calendar-view",
  head: {
        script: [{
            src: "/app/js/fullcalendar.js",
            body: true,
            crossorigin: "anonymous",
        },],
    },
  data() {
    return {
      userdetails: null,
      list: [],
      eventCalendarList: [],
      alllist: [],
      teamlist: [],
      token: "",
      service: 0,
      name: "",
      date: "",
      eventslist: [],
      team: "",
      search: "",
      iscal: false,
    };
  },

  beforeMount() {
    this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
    const headers = {
      Authorization: "Bearer " + this.token,
      Accept: "application/json",
      "Content-Type": "application/json",
    };

    this.getListBranch();

    const axios = require("axios").default;
    axios
      .get(
        `${this.$axios.defaults.baseURL}` + "patient-appointment-details/list?branch_id="+this.userdetails.branch.branch_id,
        { headers }
      )
      .then((resp) => {
        this.list = resp.data.list;
        this.alllist = resp.data.list;
         this.teamlist = resp.data.list123;
        this.Calender();
        setTimeout(() => {
          this.OnSearch();
        }, 100);
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
    async getListBranch(){
            this.loader = true;
        this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
        const headers = {
            Authorization: "Bearer " + this.userdetails.access_token,
            Accept: "application/json",
            "Content-Type": "application/json",
        };
        const axios = require("axios").default;
        axios
            .post(
                `${this.$axios.defaults.baseURL}` +
                "calendar-management/getAnnouncementList-branch",{branch_id:this.userdetails.branch.branch_id}, {
                    headers
                }
            )
            .then((resp) => {
                this.eventCalendarList = resp.data.list;
                this.loader = false;

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
                this.$swal.fire({
                    icon: 'error',
                    title: 'Oops... Something Went Wrong!',
                    text: 'the error is: ' + err,
                    footer: ''
                });
            });
        },
    Calender() {

      this.eventslist = [];
      this.list.forEach((value, index) => {
        var obj = {};
        obj.start = value.appointment_date;
        obj.end = value.appointment_date;
        obj.title = value.appointment_time + " #" + value.nric_no;
        this.eventslist.push(obj);
      });
      this.eventCalendarList.forEach((value, index) => {
        var obj = {};
        obj.start = value.start_date;
        obj.end = value.end_date;
        obj.title = value.name;
        this.eventslist.push(obj);
      });
      console.log('array list for calendar all :'+JSON.stringify(this.eventslist));
      var calendarEl = document.getElementById("calendar");
      var calendar = new FullCalendar.Calendar(calendarEl, {
        height: "550px",
        headerToolbar: {
          left: "title",
          center: "",
          right: "today prev,next",
        },

        navLinks: true, // can click day/week names to navigate views
        businessHours: true, // display business hours
        editable: true,
        selectable: true,
        events: this.eventslist,
      });
      calendar.render(this.eventslist, true);
      this.iscal=true;
    },
    OnSearch() {
       console.log(this.search , this.team);
      this.eventslist = [];
      if (this.search && this.team) {
        this.list = this.alllist.filter((notChunk) => {
          return (
            (notChunk.patient_mrn
              .toLowerCase()
              .indexOf(this.search.toLowerCase()) > -1 ||
            notChunk.name_asin_nric
              .toLowerCase()
              .indexOf(this.search.toLowerCase()) > -1 ||
            notChunk.nric_no.toLowerCase().indexOf(this.search.toLowerCase()) >
              -1 ||
            notChunk.passport_no
              .toLowerCase()
              .indexOf(this.search.toLowerCase()) > -1) &&
            (notChunk.team_name.toLowerCase().indexOf(this.team.toLowerCase()) >
              -1)
          );
        });
        this.Calender();
      } else if (this.search && !this.team) {
        this.list = this.alllist.filter((notChunk) => {
          return (
            notChunk.patient_mrn
              .toLowerCase()
              .indexOf(this.search.toLowerCase()) > -1 ||
            notChunk.name_asin_nric
              .toLowerCase()
              .indexOf(this.search.toLowerCase()) > -1 ||
            notChunk.nric_no.toLowerCase().indexOf(this.search.toLowerCase()) >
              -1 ||
            notChunk.passport_no
              .toLowerCase()
              .indexOf(this.search.toLowerCase()) > -1
          );
        });
        this.Calender();
      } else if (!this.search && this.team) {

        this.list = this.alllist.filter((notChunk) => {
          return (
            notChunk.team_name.toLowerCase().indexOf(this.team.toLowerCase()) >
            -1
          );
        });
        setTimeout(() => {
          console.log('this.list',this.list);
           this.Calender();
        }, 200);

      } else {
         this.Calender();
        this.list = this.alllist;
      }
    },
  },
};
</script>
