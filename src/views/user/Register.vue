<template>
  <div>
    <section class="bg-gray-50 dark:bg-gray-900">
      <div
        class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0"
      >
        <a
          href="#"
          class="flex items-center mb-6 text-2xl font-semibold text-gray-900 dark:text-white"
        >
          <img
            class="w-32 h-12 mr-2"
            src="https://theme.hstatic.net/200000326645/1000824936/14/logo.png?v=260"
            alt="logo"
          />
        </a>
        <div
          class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700"
        >
          <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
            <h1
              class="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white"
            >
              Create an account
            </h1>
            <form class="space-y-4 md:space-y-6" @submit.prevent="registerUser">
              <div>
                <label
                  for="username"
                  class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                  >Username</label
                >
                <input
                  v-model="username"
                  type="text"
                  name="username"
                  id="username"
                  placeholder="username"
                  class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                 
                />
                <p v-if="error.username" class="text-white  bg-red-600 text-sm py-[3px] px-4 rounded-md" >{{ error.username }}</p>
              </div>

              <div>
                <label
                  for="email"
                  class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                  >Your email</label
                >
                <input
                  v-model="email"
                  type="email"
                  name="email"
                  id="email"
                  placeholder="name@company.com"
                  class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                
                />
                <p v-if="error.email" class="text-white  bg-red-600 text-sm py-[3px] px-4 rounded-md" >{{ error.email}}</p>
              </div>

              <div>
                <label
                  for="password"
                  class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                  >Password</label
                >
                <input
                  v-model="password"
                  type="password"
                  name="password"
                  id="password"
                  placeholder="••••••••"
                  class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
              
                />
                <p v-if="error.password" class="text-white  bg-red-600 text-sm py-[3px] px-4 rounded-md" >{{ error.password }}</p>
              </div>

              <div class="flex items-start">
                <div class="flex items-center h-5">
                  <input
                    id="terms"
                    aria-describedby="terms"
                    type="checkbox"
                    class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-primary-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-primary-600 dark:ring-offset-gray-800"
                  />
                </div>
                <div class="ml-3 text-sm">
                  <label
                    for="terms"
                    class="font-light text-gray-500 dark:text-gray-300"
                    >I accept the
                    <a
                      class="font-medium text-primary-600 hover:underline dark:text-primary-500"
                      href="#"
                      >Terms and Conditions</a
                    ></label
                  >
                </div>
              </div>
           
              <button
                type="submit"
                class="w-full py-2 flex justify-center items-center text-white font-medium rounded-xl bg-yellow-600 hover:bg-yellow-700"
              >
                Create an account
              </button>
              <p class="text-sm font-light text-gray-500 dark:text-gray-400">
                Already have an account?
                <router-link
                  class="font-medium text-primary-600 hover:underline dark:text-primary-500"
                  to="/login"
                  >Login here</router-link
                >
              </p>
            </form>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      username: "",
      email: "",
      password: "",
      error : {}
    };
  },
  methods: {
    registerUser() {
      // Tạo một đối tượng từ dữ liệu người dùng
      const userData = {
        username: this.username,
        email: this.email,
        password: this.password,
      };

      // Gửi yêu cầu POST đăng ký người dùng
      axios
        .post("https://toytoytoy.onrender.com/auth/register", userData)
        .then((response) => {
            this.$router.push({ name: 'login' });
          console.log(response);
        })
        .catch((error) => {
          this.error = error.response.data;
        });
    },
  },
};
</script>
