<template>
  <div>
    <div class="top-blocks-headers d-flex justify-content-between px-5">
      <div class="text-left">
        <h3>Вещи у пользователя</h3>
      </div>
      <div class="text-right">
        <h3>Вещи на выбор</h3>
      </div>
    </div>
    <div class="top-blocks p-5">
      <b-collapse class="top-block-left top-block" visible id="collapse-3">
        <b-card>
          <div v-if="!selectedItemsOfCustomer.length">
            Вы не выбрали товары
          </div>
          <div class="row" v-else>
            <div @click="selectCustomerItem(key, 'selectedItemsOfCustomer', 'itemsOfCustomer')"
                 class="col-4 pt-3 item cursor-pointer" v-for="(item, key) in selectedItemsOfCustomer" :key="key">
              <b-collapse visible id="collapse-3">
                <b-card>
                  {{ item.name }}
                </b-card>
              </b-collapse>
            </div>
          </div>
        </b-card>
      </b-collapse>
      <b-collapse class="top-block-right top-block" visible id="collapse-3">
        <b-card>
          <div v-if="!selectedItemOfChoose.length">
            Вы не выбрали товары
          </div>
          <div class="row" v-else>
            <div @click="selectCustomerItem(key, 'selectedItemOfChoose', 'itemsOfChoose')"
                 class="col-4 pt-3 item cursor-pointer" v-for="(item, key) in selectedItemOfChoose" :key="key">
              <b-collapse visible id="collapse-3">
                <b-card>
                  {{ item.name }}
                </b-card>
              </b-collapse>
            </div>
          </div>
        </b-card>
      </b-collapse>
    </div>
    <div class="bottom-blocks p-5">
      <b-collapse class="bottom-block-left bottom-block" visible id="collapse-3">
        <b-card class="block-card">
          <div class="row">
            <div @click="selectCustomerItem(key, 'itemsOfCustomer', 'selectedItemsOfCustomer')"
                 class="col-3 pt-3 item cursor-pointer" v-for="(item, key) in itemsOfCustomer" :key="key">
              <b-collapse visible id="collapse-3">
                <b-card>
                  {{ item.name }}
                </b-card>
              </b-collapse>
            </div>
          </div>
        </b-card>
      </b-collapse>
      <b-collapse class="bottom-block-right bottom-block" visible id="collapse-3">
        <b-card class="block-card">
          <div class="row">
            <div @click="selectCustomerItem(key, 'itemsOfChoose', 'selectedItemOfChoose')"
                 class="col-3 pt-3 item cursor-pointer" v-for="(item, key) in itemsOfChoose" :key="key">
              <b-collapse visible id="collapse-3">
                <b-card>
                  {{ item.name }}
                </b-card>
              </b-collapse>
            </div>
          </div>
        </b-card>
      </b-collapse>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import {BootstrapVue, IconsPlugin} from 'bootstrap-vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

Vue.use(BootstrapVue)
Vue.use(IconsPlugin)
import Swal from 'sweetalert2'

export default {
  name: "MainPageComponent",
  data() {
    return {
      itemsOfCustomer: [
        {
          "id": 1,
          "name": "Shoes 1"
        },
        {
          "id": 2,
          "name": "Shoes 2"
        },
        {
          "id": 3,
          "name": "Shoes 3"
        },
        {
          "id": 4,
          "name": "Shoes 4"
        },
        {
          "id": 5,
          "name": "T-shirt 1"
        },
        {
          "id": 6,
          "name": "T-shirt 2"
        },
        {
          "id": 7,
          "name": "T-shirt 3"
        },
        {
          "id": 8,
          "name": "T-shirt 4"
        }
      ],
      itemsOfChoose: [
        {
          "id": 11,
          "name": "Jacket 1"
        },
        {
          "id": 12,
          "name": "Jacket 2"
        },
        {
          "id": 13,
          "name": "Jacket 3"
        },
        {
          "id": 14,
          "name": "Jacket 4"
        },
        {
          "id": 15,
          "name": "Hoodie 1"
        },
        {
          "id": 16,
          "name": "Hoodie 2"
        },
        {
          "id": 17,
          "name": "Hoodie 3"
        },
        {
          "id": 18,
          "name": "Hoodie 4"
        }
      ],
      selectedItemsOfCustomer: [],
      selectedItemOfChoose: []
    }
  },
  methods: {
    selectCustomerItem(key, firstArray, secondArray) {
      if (firstArray === 'itemsOfCustomer' && this.selectedItemsOfCustomer.length === 6) {
        Swal.fire({
          position: 'center',
          icon: 'error',
          title: 'У вас уже есть 6 товаров',
          showConfirmButton: false,
          timer: 2000
        });
      } else if (firstArray === 'itemsOfChoose' && this.selectedItemOfChoose.length === 1) {
        Swal.fire({
          position: 'center',
          icon: 'error',
          title: 'У вас уже есть 1 товар',
          showConfirmButton: false,
          timer: 2000
        });
      } else {
        this[secondArray].push(this[firstArray][key]);
        this[firstArray].splice(key, 1);
      }
    }
  }
}
</script>

<style scoped>
.top-blocks {
  display: flex;
  justify-content: space-between;
}

.top-block {
  width: 30%;
}

.bottom-blocks {
  display: flex;
  justify-content: space-between;
}

.bottom-block {
  width: 45%;
  height: 500px;
}

.block-card {
  height: 500px;
}

.cursor-pointer {
  cursor: pointer;
}
</style>