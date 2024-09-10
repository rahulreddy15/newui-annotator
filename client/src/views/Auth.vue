<template>
  <div class="bg-light login-bg">
    <div class="album py-5 container-fluid">
      <div class="row">
        <div class="col-sm">
          <div class="login-section">
            <img src="../assets/annotaPicLogo.svg"/>
            <div id="login"  v-show="totalUsers !== 0">
              <div class="login-lable" >
                  Login
              </div>
              <form class="vld-parent" ref="loginForm">
                <div class="form-group">
                  <label>Username</label>
                  <input v-model="loginForm.username" type="text" class="form-control" required />
                  <div class="invalid-feedback">Invalid username format</div>
                </div>
                <div class="form-group">
                  <label>Password</label>
                  <input v-model="loginForm.password" type="password" class="form-control" />
                </div>
                <button type="submit" class="btn btn-primary btn-block" :class="{ disabled: !loginValid }"
                  @click.prevent="loginUser">
                  Login
                </button>
                <div>New user create a account</div>
              </form>
            </div>
            <div class="" id="register" v-show="showRegistrationForm">
              <div class="login-lable" >
                  Register
              </div>
              <div v-if="!showRegistrationForm">
                You are not allowed to register new accounts
              </div>
              <form v-else class="vld-parent" ref="registerForm">
                <div class="form-group" novalidate="">
                  <label>Full Name <span class="text-mute">(Optional)</span></label>
                  <input v-model="registerForm.name" type="text" class="form-control" />
                </div>

                <div class="form-group">
                  <label>Username</label>
                  <input v-model="registerForm.username" :class="inputUsernameClasses(registerForm.username)"
                    type="text" class="form-control" required />
                  <div class="invalid-feedback">Invalid username format</div>
                </div>

                <div class="form-group">
                  <label>Password</label>
                  <input v-model="registerForm.password" :class="inputPasswordClasses(registerForm.password)"
                    type="password" class="form-control" required />
                  <div class="invalid-feedback">
                    Minimum length of 5 characters.
                  </div>
                </div>

                <div class="form-group">
                  <label>Confirm Password</label>
                  <input v-model="registerForm.confirmPassword" :class="{
                    'is-valid':
                      registerForm.confirmPassword.length > 0 &&
                      registerForm.confirmPassword === registerForm.password
                  }" type="password" class="form-control" />
                </div>
                <button type="submit" class="btn btn-primary btn-block" :class="{ disabled: !registerValid }"
                  @click.prevent="registerUser">
                  Register
                </button>
                <div>Already have a account <a>Login</a></div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="login-footer">
        <div class="container-fluid">
          <div class="row">
            <div class="col-4 footer-img-set">
              <div class="d-flex">
                <div><img src="../assets/catalog.svg" /></div>
                <div>
                  <p>Catalog</p>
                  <div>Surface and prioritize the most important data for labeling.</div>
                </div>
              </div>
            </div>

            <!-- <div class="col-4 footer-img-set">
              <div class="d-flex">
                <div><img src="../assets/model.svg" /></div>
                <div>
                  <p>Model</p>
                  <div>Test and evaluate models and mine rare examples to boost model performance.</div>
                </div>
              </div>
            </div> -->

            <div class="col-4 footer-img-set">
              <div class="d-flex">
                <div><img src="../assets/annotate.svg" /></div>
                <div>
                  <p>Annotate</p>
                  <div>Access a full suite of labeling, collaboration, and quality tools across a variety of data types.
                  </div>
                </div>
              </div>
            </div>


          </div>
        </div>
      </div>

    </div>

  </div>

</template>

<script>
import toastrs from "@/mixins/toastrs";
import { mapActions, mapMutations } from "vuex";

export default {
  name: "Authentication",
  mixins: [toastrs],
  props: {
    redirect: {
      type: Object,
      default() {
        return { name: "datasets" };
      }
    }
  },
  data() {
    return {
      activeTab: "login",
      registerForm: {
        loading: false,
        name: "",
        username: "",
        password: "",
        confirmPassword: ""
      },
      loginForm: {
        loading: false,
        username: "",
        password: ""
      }
    };
  },
  methods: {
    ...mapActions("user", ["register", "login"]),
    ...mapMutations("info", ["increamentUserCount"]),
    registerUser() {
      // Implementation remains the same
    },
    loginUser() {
      // Implementation remains the same
    },
    validUsername(username) {
      // Implementation remains the same
    },
    validPassword(password) {
      // Implementation remains the same
    },
    inputUsernameClasses(username) {
      // Implementation remains the same
    },
    inputPasswordClasses(password) {
      // Implementation remains the same
    }
  },
  computed: {
    registerValid() {
      // Implementation remains the same
    },
    loginValid() {
      // Implementation remains the same
    },
    totalUsers() {
      return this.$store.state.info.totalUsers;
    },
    allowRegistration() {
      return this.$store.state.info.allowRegistration;
    },
    showRegistrationForm() {
      return this.totalUsers === 0 || this.allowRegistration;
    },
    isAuthenticatePending() {
      return this.$store.state.user.isAuthenticatePending;
    }
  },
  watch: {
    totalUsers(users) {
      if (users === 0) {
        this.activeTab = 'register';
      }
    },
    isAuthenticatePending: {
      handler() {
        if (this.isAuthenticatePending) {
          this.$router.push({
            name: "datasets"
          });
        }
      },
      immediate: true
    }
  },
  mounted() {}
};
</script>

<style scoped>
/* Existing styles remain unchanged */

.tabs {
  display: flex;
  justify-content: space-around;
  margin-bottom: 20px;
}

.tabs button {
  background: none;
  border: none;
  color: #C9C9C9;
  font-size: 18px;
  font-weight: bold;
  padding: 10px 20px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.tabs button.active {
  color: #fff;
  border-bottom: 2px solid #6E5EEA;
}

.login-label {
  color: #C9C9C9;
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 30px;
}
</style>
