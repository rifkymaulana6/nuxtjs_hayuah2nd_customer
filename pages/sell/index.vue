<template>
    <div>
        <Nav/>
        <v-container>
          <v-card rounded="lg" class="pa-md-10 pa-5 text-center" color="primary" dark>
            <h2 class="text-md-h3">Sell Your Item</h2>
            <br/>
            <form>
                <v-text-field v-model="name"
                label="Product Name"
                outlined
                clearable></v-text-field>
                <v-text-field v-model="brand"
                label="Brand"
                outlined
                clearable></v-text-field>
                <v-text-field v-model="price"
                label="Price"
                outlined
                clearable></v-text-field>
                <v-text-field v-model="phone"
                label="WhatsApp Number"
                outlined
                clearable></v-text-field>
                <v-textarea v-model="flaws"
                      outlined
                      name="flaws"
                      label="Flaws"
                ></v-textarea>
                <v-file-input v-model="image"
                label="Picture"
                filled
                prepend-icon="mdi-camera"
              ></v-file-input>
              <v-btn
              @click="submitHandler"
                  class="mr-4 font-weight-bold"
                  color="success"
                >
                  submit
                </v-btn>
                <!-- <v-btn color="error" class="font-weight-bold">
                  clear
                </v-btn> -->
            </form>
          </v-card>
        </v-container>
        <Footer/>
        <ScrollTop/>
      </div>
</template>

<script>
import 'sweetalert2/dist/sweetalert2.min.css';
export default {
  data() {
      return {
          name: null,
          brand: null,
          price: null,
          phone: null,
          flaws: null,
          image: null,
          message: null
      }
  },
  methods:{
    async submitHandler() {
      const data = {
        'name': this.name,
        'brand': this.brand,
        'price': this.price,
        'phone': this.phone,
        'flaws': this.flaws,
        'image': this.image
      }
      try {
        const res = await this.$axios.post('/sells', data, {
          headers: {
            'Content-type': 'multipart/form-data'
          }
        })
        // this.message = res.data.message
        this.$swal({
            toast: true,
            text: "Your item has been successfully uploaded",
            icon: 'success',
            timer: 4000,
            timerProgressBar: true,
            showConfirmButton: false,
            position: 'top-end',
        });
        this.$router.push('/products')
      } catch (e) {
        this.error = e.response.data.message
      }
    },
  }
}
</script>

<style>

</style>