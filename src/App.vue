<template>
  <div id="app">
    <div class="wrap">
      <div class="users-list">
        <!-- list -->

        <h2 class="list__title">List</h2>

        <div class="list__block">
          <ul class="list__block_users">
            <li
              v-for="(user, index) in users"
              :key="index"
              class="lb_item list__block_users_item"
              :class="{ 'lb_ext-active': current === index }"
            >
              <div class="list">
                <div class="list__full-name">
                  <p class="list__full-name_name">{{ user.name }}</p>
                  <p class="flist__ull-name_city">{{ user.address.city }}</p>
                </div>
                <div class="buttons">
                  <p class="buttons__number">#{{ user.id }}</p>
                  <button
                    class="buttons__btn buttons__btn_wiew"
                    @click="selectUser(index)"
                  >
                    view
                  </button>
                  <button
                    class="buttons__btn buttons__btn_delete"
                    @click="removeUser(index)"
                  >
                    delete
                  </button>
                </div>
              </div>
              <transition
                mode="out-in"
                name="faq-fade"
                :before-enter="beforeEnter"
                :enter="enter"
              >
                <UserDetail :user_detail="user" v-show="current === index" />
              </transition>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UserDetail from "@/components/UserDetail";
import axios from "axios";
export default {
  components: {
    UserDetail,
  },
  data() {
    return {
      users: [],
      current: -10,
    };
  },
  created() {
    this.getFolders();
  },
  methods: {
    selectUser(newUser) {
      if (newUser === this.current) {
        this.current = -10;
      } else {
        this.current = newUser;
      }
    },
    beforeEnter(_t) {
      _t.style.display = "block";
      _t.style.maxHeight = null;
      _t.myHeight = _t.offsetHeight;
      _t.style.maxHeight = 0;
      _t.style.display = null;
    },
    enter(_t) {
      _t.style.maxHeight = _t.myHeight + "px";
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
