<template>
  <div id="layoutSidenav">

    <div id="layoutSidenav_content" class="ml-0">

      <main>
        <Loader v-if="loader" />
        <div class="container-fluid px-4">
          <div class="card mb-4 mt-3">
            <div class="card-header">
              <h4>Volunteer, Outreach, And Networking Application Form</h4>
              <a href="#" class="visibility-h"
                ><i class="fa fa-user-edit"></i
              ></a>
            </div>
            <div class="card-body mt-3">
              <p>
                MENTARI encourages the participation of any individual, group,
                or organization (government or private) to enhance service
                delivery related to mental health. The information provided
                through this form will be kept confidential and will help us
                determine the most satisfying volunteer or networking
                opportunity for you.
              </p>

              <div class="row">
                <div class="col-lg-4 col-sm-6">
                  <div class="mb-3">
                    <label for="" class="form-label">Application Form</label>
                    <select v-model="selectForm" class="form-select select-others" aria-label="">
                      <option value="0">Select Application Form</option>
                      <option value="individual">Individual</option>
                      <option value="group">Group</option>
                      <option value="organization">Organization</option>
                    </select>
                  </div>
                </div>
              </div>
              <div v-if="this.selectForm == 'individual'">
              <Individual />
              </div>

              <!-- individual -->

              <div v-if="this.selectForm == 'group'">
              <Group />
              </div>
              <!-- group -->

              <div v-if="this.selectForm == 'organization'">
              <Organization />
              </div>
              <!-- Organization -->
            </div>
          </div>
        </div>
      </main>
      <von-footer></von-footer>
    </div>
  </div>
</template>
<script>
import Group from "../components/Von/public-Group.vue";
import Individual from "../components/Von/public-Individual.vue";
import Organization from "../components/Von/public-Organization.vue";
import VonFooter from "../components/Von/VonFooter.vue";
import VonHeader from "../components/Von/VonHeader.vue";
import VonSidebar from "../components/Von/VonSidebar.vue";
export default {
  components: {
    VonSidebar,
    VonHeader,
    VonFooter,
    Individual,
    Group,
    Organization,
  },
  name: "von-management",
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
      errors: [],
      loader: false,
      selectForm: "",
    };
  },
  beforeMount() {
  },
};
</script>

<style scoped>
.hide {
  display: none;
}
</style>
