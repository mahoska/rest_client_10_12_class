<template>
        <div>
          <table class="table">
            <tr v-for="car in  cars"  >
              <td>
                <router-link  :to="'/carItem/'+car.id">
                  <img alt="car" class="car-img"  :src="car.img" />
                </router-link>
              </td>
              <td>{{ car.brand }}</td>
              <td>{{ car.model }}</td>
            </tr>
          </table>
        </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'carList',
  data () {
    return {
      config: {
          headers: {'Content-Type': 'application/x-www-form-urlencoded'}
      },
      cars:{},
      err_year: "",
      err_work: "",
      err_param:"",
      error_str : "We apologize, we have temporary problems with the service. return to us later"
  }
},
  created(){			
        var self = this
        //axios.get('http://localhost:88/REST/client/api/cars/', this.config)
         axios.get('http://192.168.0.15/~user15/REST/client/api/cars/', this.config)
              .then(function (response) {
                  self.cars = response.data['data'].cars
                  //this.$parent.$options.methods.clearFilter();
                  self.$emit('clear')
        })
        .catch(function (error) {
          console.log(error);
        });
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.car-img{
   max-height:100px;
   max-width:100px;
   cursor:pointer;
}



</style>
