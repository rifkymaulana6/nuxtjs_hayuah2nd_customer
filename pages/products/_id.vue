<template>
    <div>
        <Nav/>
        <v-container v-if="product">
            <v-row justify="center">
                <v-col cols="11" md="7">
                    <h2 class="text-center text-md-h4 font-weight-bold">
                        {{product.title}}
                    </h2>
                    <!-- <div class="text-center mt-2">
                        <v-rating readonly half-increments class="mb-2" color="yellow darken-2" background-color="gray lighten-1" :value="product.ratings" dense size="20"></v-rating>
                        <v-chip x-small label outlined class="mr-1" v-for="(t, i) in product.tags" :key="`prod${product.id}-${i}`">
                            {{ t }}
                        </v-chip>
                    </div> -->
                    <br/>
                    <v-img width="100%" class="el rounded-lg" height="50vh" :src="product.image"></v-img>
                    <p class="mt-5 mb-7">
                        {{ product.full_description }}
                    </p>
                        <v-dialog
                          v-model="dialog"
                          persistent
                          max-width="600px"
                        >
                          <template v-slot:activator="{ on, attrs }">
                            <v-btn
                              color="green"
                              dark
                              v-bind="attrs"
                              v-on="on"
                            >
                            <v-icon size="20" color="white" class="mr-2">mdi-whatsapp</v-icon>
                            <span color="white">Go To WhatsApp</span>
                            </v-btn>
                          </template>
                          <v-card>
                            <v-card-title>
                              <span class="text-h5">Enter Your Bid</span>
                            </v-card-title>
                            <v-card-text>
                              <v-container>
                                <v-row>
                                  <v-col
                                    cols="12"
                                    sm="6"
                                    md="4"
                                  >
                                    <v-text-field v-model="bid"
                                      label="Your bid*"
                                      required
                                    ></v-text-field>
                                  </v-col>
                                </v-row>
                              </v-container>
                              <small>*indicates required field</small>
                            </v-card-text>
                            <v-card-actions>
                              <v-spacer></v-spacer>
                              <v-btn
                                color="red"
                                text
                                @click="dialog = false"
                              >
                                Close
                              </v-btn>
                              <v-btn
                              @click="sendHandler"
                                color="green"
                                text
                                target="_blank"
                                :href="url"
                              >
                                Send
                              </v-btn>
                            </v-card-actions>
                          </v-card>
                        </v-dialog>
                    <!-- <v-btn @click="$store.commit(`cart/AddToCart`, product)" min-height="45" min-width="170" class="text-capitalize" color="green">
                        <v-icon size="20" color="white">mdi-whatsapp</v-icon>
                        <span color="white">Go To WhatsApp</span>
                    </v-btn> -->
                </v-col>
            </v-row>
        </v-container>
        <br/><br/>
        <Footer/>
        <ScrollTop/>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    async asyncData ({params}) {
        const { data } = await axios.get(`http://localhost:8000/api/products/${params.id}`)
        return {
            product: data
        }
    },

    data: () => ({
      dialog: false,
      bid: null,
      url: ''
    }),

    methods: {
        async sendHandler() {
            const id = this.$route.fullPath.split('/').slice(-1).pop()
            const { data: product } = await axios.get(`http://localhost:8000/api/products/${id}`)
            const data = {
                'bid': this.bid,
            }
            this.url = 'https://api.whatsapp.com/send?phone=6282126201022&text=Saya%20memberi%20tawaran%20Rp.%20' + data.bid + '%20untuk%20' + product.title + ' ' + window.location.href
        }
    },

}
</script>

<style>

</style>