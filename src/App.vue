<template>
  <div id="app">
    <div class="wrap">
      <div class="users-list">
        <!-- list -->
        <div class="list">
          <h2 class="list__title">List</h2>
          <div class="list__block">
            <ul
              class="list__block_users"
              v-for="(user, index) in users"
              :key="index"
            >
              <li class="list__block_users_item">
                <div class="full-name">
                  <p class="full-name__name">{{ user.name }}</p>
                  <p class="full-name__city">{{ user.address.city }}</p>
                </div>
                <div class="buttons">
                  <p class="buttons__number">#{{ user.id }}</p>
                  <button
                    class="buttons__btn buttons__btn_wiew"
                    @click="selectUser(index)"
                  >
                    wiew
                  </button>
                  <button
                    class="buttons__btn buttons__btn_delete"
                    @click="removeUser"
                  >
                    delete
                  </button>
                </div>
              </li>
            </ul>
          </div>
        </div>
        <!-- user wiew -->
        <div class="view-block" v-if="visible">
          <div class="wiew" v-for="(user, index) in users" :key="index">
            <div class="wiew__full-name bl">
              <h2 class="wiew__full-name_name">{{ user.name }}</h2>
              <p class="wiew__full-name_id">
                <span>id: {{ user.id }} |</span>
                <span> username: {{ user.username }} |</span>
                <span> email: {{ user.email }}</span>
              </p>
            </div>
            <div class="wiew__adress bl">
              <h3 class="wiew__adress_title title">Address</h3>
              <p class="wiew__adress_ad">
                {{ user.address.zipcode }}
                {{ user.address.street }}
                {{ user.address.city }}
                {{ user.address.suite }}
              </p>
              <p class="wiew__adress_geo">
                Geo:
                <span
                  >Lat {{ user.address.geo.lat }} Lng
                  {{ user.address.geo.lng }}</span
                >
              </p>
            </div>
            <div class="wiew__phone bl">
              <h3 class="wiew__phone_title title">Phone</h3>
              <p class="wiew__phone_phone">{{ user.phone }}</p>
            </div>
            <div class="wiew__website bl">
              <h3 class="wiew__website_title title">Website</h3>
              <a href="#" class="wiew__website_web">{{ user.website }}</a>
            </div>
            <div class="wiew__company bl">
              <h3 class="wiew__company_title title">Company</h3>
              <p class="wiew__company_text">
                {{ user.company.name }}
              </p>
              <p class="wiew__company_subtext">
                {{ user.company.catchPhrase }} <br />{{ user.company.bs }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      users: [],
      visible: false,
    };
  },
  created() {
    this.getFolders();
  },
  methods: {
    selectUser(index) {
      if (index === 0) {
        console.log(index);
      } else {
        console.log("index");
      }

      this.visible = !this.visible;
    },
    removeUser(x) {
      this.users.splice(x, 1);
    },
    async getFolders() {
      await axios
        .get("https://jsonplaceholder.typicode.com/users")
        .then((response) => {
          this.users = response.data.slice(0, 5);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style scoped>
@import "@/assets/style.css";
</style>
