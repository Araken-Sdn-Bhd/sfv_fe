<template>
<div id="layoutSidenav">
    <CommonSidebar />
    <div id="layoutSidenav_content">
        <CommonHeader />
        <main>
            <!-- <Loader v-if="loader" /> -->
            <div class="container-fluid px-4">
                <div class="page-title">
                    <h1>SE Consent Form</h1>
                    <!-- <a href="#"><i class="fal fa-plus"></i> Add</a> -->
                </div>
                <div class="card mb-4" v-if="consentdetails">
                    <div class="form-header">
                        <img src="~/assets/images/form-logo.png" />
                        <h2> [{{ this.hospitalName }}]</h2>
                        <p>
                            Hospital Borang Persetujuan Menyertai Program Sokongan Pekerjaan
                        </p>
                    </div>
                    <div class="card-body new-form">
                        <div class="form-title">
                            <h5>1. CONSENT FOR PARTICIPATION</h5>
                        </div>
                        <table class="notes table-padding flex-table">
                            <tbody class="d-m-block">
                                <tr class="d-m-block">
                                    <td colspan="2">
                                        <div class="form-check">
                                            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault" v-model="participant" />
                                            <label class="form-check-label label-balck" for="flexCheckDefault">
                                                I hereby agree to participate in supported employment
                                                program,<strong>[{{ this.branchName }}]</strong>. I also agree to
                                                follow the rules and give my full commitment. I fully
                                                understand if any rules was not follow, I deemed to be
                                                terminated from this program.
                                            </label>
                                        </div>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <table class="mt-3">
                                            <tbody>
                                                <tr>
                                                    <th>Patient/Guardian:</th>
                                                    <td>{{ consentdetails.patient_name }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Witness:</th>
                                                    <td>{{ consentdetails.user_name }}</td>
                                                    <!-- <td> <input type="text" class="form-control" name="" v-model="consentdetails.user_name" /></td> -->
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>NRIC No:</th>
                                                    <td>{{ consentdetails.nric_no }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Designation:</th>
                                                    <td>{{ consentdetails.designation}}</td>
                                                    <!-- <td><input type="text" class="form-control" v-model="consentdetails.designation"> </td> -->
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Date:</th>
                                                    <td>{{ consentdetails.date }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Date:</th>
                                                    <td>{{ consentdetails.date }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                        <div class="form-title">
                            <h5>2. CONSENT FOR DISCLOSURE</h5>
                        </div>
                        <table class="notes table-padding flex-table">
                            <tbody class="d-m-block">
                                <tr class="d-m-block">
                                    <td colspan="2">
                                        <span>I agree and consent for <strong>[{{ this.branchName }}]</strong> to
                                            disclose my medical record to employee and will not
                                            subjected to any act related uder the law.</span>
                                    </td>
                                </tr>
                                <tr>
                                  <td colspan="2">
                                        <div v-if="this.type != 'view'">
                                            <div class="form-check form-check-inline mt-2">
                                                <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio1" value="1" v-model="discloser" />
                                                <label class="form-check-label" for="inlineRadio1">Yes
                                                </label>
                                            </div>
                                            <div class="form-check form-check-inline mt-2">
                                                <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio2" value="0" v-model="discloser" />
                                                <label class="form-check-label" for="inlineRadio2">No
                                                </label>
                                            </div>
                                        </div>
                                        <div v-if="this.type == 'view'">
                                            <div v-if="this.discloser == 1">
                                                <div class="form-check form-check-inline mt-2">
                                                    <input class="form-check-input" type="radio" name="inlineRadioOptions3" id="inlineRadio1" value="1" checked />
                                                    <label class="form-check-label" for="inlineRadio1">Yes
                                                    </label>
                                                </div>
                                                <div class="form-check form-check-inline mt-2">
                                                    <input class="form-check-input" type="radio" name="inlineRadioOptions4" id="inlineRadio2" value="0"  />
                                                    <label class="form-check-label" for="inlineRadio2">No
                                                    </label>
                                                </div>
                                            </div>
                                            <div v-if="this.discloser == 0">
                                                <div class="form-check form-check-inline mt-2">
                                                    <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio1" value="1" />
                                                    <label class="form-check-label" for="inlineRadio1">Yes
                                                    </label>
                                                </div>
                                                <div class="form-check form-check-inline mt-2">
                                                    <input class="form-check-input" type="radio" name="inlineRadioOptions2" id="inlineRadio2" value="0" checked />
                                                    <label class="form-check-label" for="inlineRadio2">No
                                                    </label>
                                                </div>
                                            </div>
                                        </div>
                                    </td>
                                </tr>

                                <tr>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Patient/Guardian:</th>
                                                    <td>{{ consentdetails.patient_name }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Witness:</th>
                                                    <td>{{ consentdetails.user_name }}</td>
                                                    <!-- <td> <input type="text" class="form-control" name="" v-model="consentdetails.user_name" /></td> -->
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>NRIC No:</th>
                                                    <td>{{ consentdetails.nric_no }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Designation:</th>
                                                    <td>{{ consentdetails.designation }}</td>
                                                    <!-- <td> <input type="text" class="form-control" name="" v-model="consentdetails.designation" /></td> -->
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Date:</th>
                                                    <td>{{ consentdetails.date }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Date:</th>
                                                    <td>{{ consentdetails.date }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                        <p v-if="errorList.length">
                            <ul>
                                <li style="color:red" v-for='err in errorList' :key='err'>
                                    {{ err }}
                                </li>
                            </ul>
                        </p>

                    </div>
                </div>

                <div class="card mb-4 reslt" v-if="consentdetails" style="display:none;">
                    <div class="form-header">
                        <img src="~/assets/images/form-logo.png" />
                        <h2>[{{ this.hospitalName  }}]</h2>
                        <p>
                            Hospital Borang Persetujuan Menyertai Program Sokongan Pekerjaan
                        </p>
                    </div>
                    <div class="card-body new-form">
                        <div class="form-title">
                            <h5>1. CONSENT FOR PARTICIPATION</h5>
                        </div>
                        <table class="notes table-padding">
                            <tbody>
                                <tr>
                                    <td colspan="2">
                                        <div class="form-check">
                                            <input class="form-check-input" type="checkbox" value="" checked id="flexCheckDefault" v-model="participant" />
                                            <label class="form-check-label label-balck" for="flexCheckDefault">
                                                I hereby agree to participate in supported employment
                                                program, [{{ this.branchName }}]. I also agree to
                                                follow the rules and give my full commitment. I fully
                                                understand if any rules was not follow, I deemed to be
                                                terminated from this program.
                                            </label>
                                        </div>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <textarea class="signature"></textarea>
                                        <p class="text-align-center">Signature Patient/Guardian</p>
                                    </td>
                                    <td>
                                        <textarea class="signature"></textarea>
                                        <p class="text-align-center">Signature Witness</p>
                                    </td>
                                </tr>
                                <tr>

                                    <td>
                                        <table class="mt-3">
                                            <tbody>
                                                <tr>
                                                    <th>Patient/Guardian:</th>
                                                    <td>{{ consentdetails.patient_name }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Witness:</th>
                                                    <td>{{ consentdetails.user_name }}</td>

                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>NRIC No:</th>
                                                    <td>{{ consentdetails.nric_no }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Designation:</th>
                                                    <td>{{ consentdetails.designation }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Date:</th>
                                                    <td>{{ consentdetails.date }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Date:</th>
                                                    <td>{{ consentdetails.date }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                        <div class="form-title">
                            <h5>2. CONSENT FOR DISCLOSURE</h5>
                        </div>
                        <table class="notes table-padding">
                            <tbody>
                                <tr>
                                    <td colspan="2">
                                        I agree and consent for [{{ this.branchName }}] to
                                        disclose my medical record to employee and will not
                                        subjected to any act related uder the law.
                                    </td>
                                </tr>
                                <tr>
                                    <td colspan="2">
                                        <div v-if="this.discloser == 1">
                                            <div class="form-check form-check-inline mt-2">
                                                <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio1" value="1" v-model="discloser" checked />
                                                <label class="form-check-label" for="inlineRadio1">Yes
                                                </label>
                                            </div>
                                            <div class="form-check form-check-inline mt-2">
                                                <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio2" value="0" v-model="discloser" />
                                                <label class="form-check-label" for="inlineRadio2">No
                                                </label>
                                            </div>
                                        </div>
                                        <div v-if="this.discloser == 0">
                                            <div class="form-check form-check-inline mt-2">
                                                <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio1" value="1" v-model="discloser" />
                                                <label class="form-check-label" for="inlineRadio1">Yes
                                                </label>
                                            </div>
                                            <div class="form-check form-check-inline mt-2">
                                                <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio2" value="0" v-model="discloser" checked />
                                                <label class="form-check-label" for="inlineRadio2">No
                                                </label>
                                            </div>
                                        </div>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <textarea class="signature"></textarea>
                                        <p class="text-align-center">Signature Patient/Guardian</p>
                                    </td>
                                    <td>
                                        <textarea class="signature"></textarea>
                                        <p class="text-align-center">Signature Witness</p>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Patient/Guardian:</th>
                                                    <td>{{ consentdetails.patient_name }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Witness:</th>
                                                    <td>{{ consentdetails.user_name }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>NRIC No:</th>
                                                    <td>{{ consentdetails.nric_no }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Designation:</th>
                                                    <td>{{ consentdetails.designation }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Date:</th>
                                                    <td>{{ consentdetails.date }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Date:</th>
                                                    <td>{{ consentdetails.date }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                        <p v-if="errorList.length">
                            <ul>
                                <li style="color:red" v-for='err in errorList' :key='err'>
                                    {{ err }}
                                </li>
                            </ul>
                        </p>

                    </div>
                </div>
                <div class="d-flex">
                    <button @click="GoBack" class="btn btn-primary btn-text">
                        <i class="fa fa-arrow-alt-to-left"></i> Back
                    </button>
                    <div class="ml-auto" v-if="!pid">
                        <button type="button" class="btn btn-warning btn-text" @click="OnSubmit"><i class="fa fa-save"></i> Save</button>
                        <a @click="OnPrint" class="btn btn-success btn-text"><i class="fad fa-print"></i>Print</a>
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
import CommonHeader from "../../../components/CommonHeader.vue";
import CommonSidebar from "../../../components/CommonSidebar.vue";
export default {
    components: {
        CommonSidebar,
        CommonHeader
    },
    name: "patient-summary",
    data() {
        return {
            userdetails: null,
            Id: 0,
            errorList: [],
            consentdetails: null,
            hospitalName: "",
            branchName: "",
            loader: false,
            participant: 0,
            discloser: 1,
            appId: 0,
        };
    },
    beforeMount() {
        this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
        let urlParams = new URLSearchParams(window.location.search);
        this.hospitalName = this.userdetails.branch.hospital_name;
        this.branchName = this.userdetails.branch.hospital_branch_name;
        this.Id = urlParams.get("id");
        this.appId = urlParams.get("appId");
        if (this.Id) {
            this.GetPatientConnsentdetails();
        }
        let urlParams1 = new URLSearchParams(window.location.search);
        this.pid = urlParams1.get("pid");
        this.type = urlParams1.get("type");
        if (this.pid) {
            this.getdetails();
        }
    },
    methods: {
        async GetPatientConnsentdetails() {
            this.loader = true;
            const headers = {
                Authorization: "Bearer " + this.userdetails.access_token,
                Accept: "application/json",
                "Content-Type": "application/json",
            };
            const response = await this.$axios.post(
                "intervention/get-se-form", {
                    added_by: this.userdetails.user.id,
                    patient_id: this.Id,
                    appId: this.appId,
                    pid: this.pid,
                    type: "SEConsentForm",
                }, {
                    headers
                }
            );
            console.log("my log", response.data);
            if (response.data.code == 200) {
                this.loader = false;
                this.consentdetails = response.data.list;
            } else {
                this.loader = false;
                this.$swal.fire({
                    icon: 'error',
                    title: 'Oops... Something Went Wrong!',
                    text: 'the error is: ' + this.error,
                    footer: ''
                });
            }
        },
        async OnSubmit() {
            this.errorList = [];
            try {
                if (!this.participant) {
                    this.errorList.push(
                        "Please agree to participate in supported employment program"
                    );
                  } else {
                    this.participant = "1";
                }
                if (this.participant) {
                    this.loader = true;
                    const headers = {
                        Authorization: "Bearer " + this.userdetails.access_token,
                        Accept: "application/json",
                        "Content-Type": "application/json",
                    };
                    const response = await this.$axios.post(
                        "intervention/se-form", {
                            added_by: this.userdetails.user.id,
                            patient_id: this.Id,
                            consent_for_participation: this.participant,
                            consent_for_disclosure: this.discloser,
                        }, {
                            headers
                        }
                    );
                    console.log("result", response.data);
                    if (response.data.code == 200) {
                        this.loader = false;
                        this.$swal.fire('Successfully Update', '', 'success');
                    } else {
                        this.loader = false;
                        this.$swal.fire({
                            icon: 'error',
                            title: 'Oops... Something Went Wrong!',
                            text: 'the error is: ' + JSON.stringify(response.data.message),
                            footer: ''
                        });
                    }
                }
            } catch (e) {
                this.loader = false;
                console.log("error", e);
            }
        },
        OnPrint() {
            var newstr = document.getElementsByClassName("reslt")[0].innerHTML;
            document.body.innerHTML = newstr;
            window.print();
            // Reload the page to refresh the data
            window.location.reload();
        },
        async getdetails() {
            const headers = {
                Authorization: "Bearer " + this.userdetails.access_token,
                Accept: "application/json",
                "Content-Type": "application/json",
            };
            const response = await this.$axios.post(
                "/patient-appointment-details/fetchViewHistoryListDetails", {
                    id: this.pid,
                    type: "SEConsentForm",
                }, {
                    headers
                }
            );
            if (response.data.code == 200) {

                this.Id = response.data.Data[0].patient_id;

                this.discloser = response.data.Data[0].consent_for_disclosure;
                this.participant = response.data.Data[0].consent_for_participation;

                this.GetPatientConnsentdetails();
            } else {
                this.$swal.fire({
                    icon: 'error',
                    title: 'Oops... Something Went Wrong!',
                    text: 'the error is: ' + this.error,
                    footer: ''
                });
            }
        },
        GoBack() {
          if (this.type == 'view') {
                this.$router.go(-1);
            } else {
                this.$router.push({
                    path: "/modules/Intervention/patient-summary",
                    query: {
                        id: this.Id,
                        appId: this.appId
                    },
                });
            }
        },
    },
};
</script>

<style scoped>
.hide {
    display: none;
}

.signature {
    width: 90%;
    resize: none;
    height: 95px;
    margin-top: 30px;
}

.text-align-center {
    text-align: center;
}
</style>
