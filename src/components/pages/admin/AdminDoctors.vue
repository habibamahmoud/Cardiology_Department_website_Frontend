<template>
    <admin-nav-bar></admin-nav-bar>
    <base-card>
        <h2>Doctors</h2>
        <div class="table-responsive">
            <table class="table">
                <thead>
                    <tr>
                        <th>First Name</th>
                        <th>Last Name</th>
                        <th>Age</th>
                        <th>Mobile Number</th>
                        <!-- <th>Id</th> -->
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="doctors in doctorDetails" :key="doctors.id">
                        <td>{{ doctors.first_name }}</td>
                        <td>{{ doctors.last_name }}</td>
                        <td>{{ doctors.age }}</td>
                        <td>{{ doctors.mobile }}</td>
                        <!-- <td>{{ doctors._id}}</td> -->
                    </tr>
                </tbody>
            </table>
        </div>
    </base-card>
</template>
<script>
import axios from 'axios';
export default {
  data() {
      return {
          doctorDetails: [],
      };
  },
  mounted() {
      this.getDoctorDetails();
  },
  methods: {
      getDoctorDetails() {
          axios.get(
              `http://localhost:5000/doctors`, {
                  headers: {
                      'Content-Type' : 'application/json',
                  }
              }
          ).then((response) => {
              this.formatDoctorDetails(response.data);
          });
      },
      formatDoctorDetails(doctors) {
          for (let key in doctors) {
              this.doctorDetails.push({...doctors[key], id:key});
          }
          console.log(this.doctorDetails);
      }
  }

}
</script>