<template>
<div id="layoutSidenav">
    <CommonSidebar />
    <div id="layoutSidenav_content">
        <CommonHeader />
        <main>
            <div class="container-fluid px-4" v-if="consentdetails">
                <div class="page-title">
                    <h1>CPS HOME VISIT WITHDRAWAL FORM</h1>
                </div>
                <div class="card mb-4">
                    <div class="card-body new-form">
                        <div class="form-header">
                            <img src="~/assets/images/form-logo.png" />
                            <h2>{{this.hospitalName}}</h2>
                            <p>
                                COMMUNITY PSYCHIATRY SERVICES HOME VISIT WITHDRAWAL CONSENT
                                FORM
                            </p>
                        </div>
                        <table class="notes table-padding">
                            <tbody>
                                <tr>
                                    <td colspan="2">
                                        <div class="form-check">
                                            <input class="form-check-input" type="checkbox" value="1" id="flexCheckDefault" v-model="community_psychiatry_services" />
                                            <label class="form-check-label label-balck" for="flexCheckDefault">
                                                I, as the patient's next of kin hereby withdraw
                                                consent given for Community Psychiatry Service Home
                                                Visit and psychiatry treatment for the patient. I
                                                acknowledge that my decision is againts medical
                                                advices from Doctor or Case Manager; besides, I also
                                                fully understand those risk. I hereby will be
                                                responsible for the patients's psychiatry treatement
                                                and any risks due to my decision.
                                            </label>
                                        </div>
                                    </td>
                                </tr>

                                <tr>
                                    <td>
                                        <table class="mt-3">
                                            <tbody>
                                                <tr>
                                                    <th>Patient's Name:</th>
                                                    <td>{{ consentdetails.patient_name }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Guardian:</th>
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
                                                    <th>NRIC No:</th>
                                                    <td>{{ consentdetails.guardian_nric  }}</td>
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
                                                    <th>Date :</th>
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

                        <table class="notes" v-if="consentdetails">
                            <tbody>
                                <tr>
                                    <td style="width:16%">Doctor's Name/Case Manager:</td>
                                    <td>{{ consentdetails.designation }}</td>
                                </tr>

                                <tr>
                                    <td>Date:</td>
                                    <td>{{ consentdetails.date }}</td>
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

            </div>
            <div class="container-fluid px-4 reslt" v-if="consentdetails" style="display:none;">
                <div class="page-title">
                    <h1>CPS HOME VISIT WITHDRAWAL FORM</h1>
                </div>
                <div class="card mb-4">
                    <div class="card-body new-form">
                        <div class="form-header">
                            <img src="~/assets/images/form-logo.png" />
                            <h2>{{this.hospitalName}}</h2>
                            <p>
                                COMMUNITY PSYCHIATRY SERVICES HOME VISIT WITHDRAWAL CONSENT
                                FORM
                            </p>
                        </div>
                        <table class="notes table-padding">
                            <tbody>
                                <tr>
                                    <td colspan="2">
                                        <div class="form-check">
                                            <input class="form-check-input" type="checkbox" value="1" id="flexCheckDefault" v-model="community_psychiatry_services" />
                                            <label class="form-check-label label-balck" for="flexCheckDefault">
                                                I, as the patient's next of kin hereby withdraw
                                                consent given for Community Psychiatry Service Home
                                                Visit and psychiatry treatment for the patient. I
                                                acknowledge that my decision is againts medical
                                                advices from Doctor or Case Manager; besides, I also
                                                fully understand those risk. I hereby will be
                                                responsible for the patients's psychiatry treatement
                                                and any risks due to my decision.
                                            </label>
                                        </div>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <textarea class="signature"></textarea>
                                        <p class="text-align-center">Signature Patient/Guardian</p>
                                    </td>
                                    <!-- <td>
                     <textarea class="signature"></textarea>
                      <p class="text-align-center">Doctor</p>
                      </td> -->
                                </tr>
                                <tr>
                                    <td>
                                        <table class="mt-3">
                                            <tbody>
                                                <tr>
                                                    <th>Patient's Name:</th>
                                                    <td>{{ consentdetails.patient_name }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </td>
                                    <td>
                                        <table>
                                            <tbody>
                                                <tr>
                                                    <th>Guardian:</th>
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
                                                    <th>NRIC No:</th>
                                                    <td>{{ consentdetails.guardian_nric}}</td>
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
                                                    <th>Date :</th>
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
                        <table class="notes" v-if="consentdetails">
                            <tbody>
                                <tr>
                                    <td style="width:50%">
                                        <textarea class="signature"></textarea>
                                        <p class="text-align-center">Doctor</p>
                                    </td>
                                    <td>
                                        <!-- <textarea class="signature"></textarea>
                      <p class="text-align-center">Doctor</p> -->
                                    </td>
                                </tr>
                            </tbody>
                        </table>

                        <table class="notes" style="width:50%" v-if="consentdetails">
                            <tbody>

                                <tr>
                                    <td style="width:50%">Doctor's Name/Case Manager:</td>
                                    <td>{{ consentdetails.designation }}</td>
                                </tr>

                                <tr>
                                    <td>Date:</td>
                                    <td>{{ consentdetails.date }}</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
            <p v-if="errorList.length">
                <ul>
                    <li style="color:red" v-for='err in errorList' :key='err'>
                        {{ err }}
                    </li>
                </ul>
            </p>
            <br><br>
            <div class="d-flex">
                <button @click="GoBack" class="btn btn-primary btn-text">
                    <i class="fa fa-arrow-alt-to-left"></i> Back
                </button>
                <div class="ml-auto" v-if="!pid">
                    <button type="button" class="btn btn-warning btn-text" @click="OnSubmit">
                        <i class="fa fa-save"></i> Save
                    </button>
                    <a @click="OnPrint" class="btn btn-success btn-text"><i class="fad fa-print"></i>Print</a>
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
    name: "cps-homevisit-withdrawal-form",
    data() {
        return {
            userdetails: null,
            Id: 0,
            errorList: [],
            consentdetails: null,
            hospitalName: "",
            branchName: "",
            loader: false,
            community_psychiatry_services: 0,
            pid: 0,
            type: "",
            appId: 0,
        };
    },
    beforeMount() {
        this.userdetails = JSON.parse(localStorage.getItem("userdetails"));
        let urlParams = new URLSearchParams(window.location.search);
        this.hospitalName = this.userdetails.branch.hospital_name;
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
                "intervention/get-homevisit-consent-form", {
                    added_by: this.userdetails.user.id,
                    patient_id: this.Id,
                    appId: this.appId,
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
                if (!this.community_psychiatry_services) {
                    this.errorList.push("Please accept term & condition");
                } else {
                    this.community_psychiatry_services = "1";
                }
                if (this.community_psychiatry_services) {
                    const headers = {
                        Authorization: "Bearer " + this.userdetails.access_token,
                        Accept: "application/json",
                        "Content-Type": "application/json",
                    };
                    const response = await this.$axios.post(
                        "intervention/homevisit-withdrawal-form", {
                            added_by: this.userdetails.user.id,
                            patient_id: this.Id,
                            community_psychiatry_services: this.community_psychiatry_services,
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
                    type: "CpsHomeVisitWithdrawalForm",
                }, {
                    headers
                }
            );
            if (response.data.code == 200) {

                this.Id = response.data.Data[0].patient_id;

                this.community_psychiatry_services =
                    response.data.Data[0].community_psychiatry_services;

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
