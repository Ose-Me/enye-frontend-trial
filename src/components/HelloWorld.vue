<template>
  <div class="hello">
    <div class="loader-wrapper" v-if="loading">
      <div class="loader is-loading"></div>
    </div>

    <div class="main-container" v-if="!loading">
      <div class="container py-5 px-3">
        <!-- search bar -->
        <div class="field is-grouped">
          <p class="control is-expanded has-icons-right">
            <input
              class="input"
              type="text"
              v-model="searchQuery"
              placeholder="Search..."
            />
            <span class="icon is-small is-right">
              <button>
                <img src="../assets/search-Icon.svg" alt="" />
              </button>
            </span>
          </p>

          <!-- filter icon -->
          <div class="is-flex is-align-items-center" @click="toggleFilter()">
            <svg
              height="15pt"
              viewBox="-5 0 394 394.00003"
              width="15pt"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                class="filter-btn"
                d="m367.820312 0h-351.261718c-6.199219-.0117188-11.878906 3.449219-14.710938 8.960938-2.871094 5.585937-2.367187 12.3125 1.300782 17.414062l128.6875 181.285156c.042968.0625.089843.121094.132812.183594 4.675781 6.3125 7.207031 13.960938 7.21875 21.816406v147.800782c-.027344 4.375 1.691406 8.582031 4.773438 11.6875 3.085937 3.101562 7.28125 4.851562 11.65625 4.851562 2.222656-.003906 4.425781-.445312 6.480468-1.300781l72.3125-27.570313c6.476563-1.980468 10.777344-8.09375 10.777344-15.453125v-120.015625c.011719-7.855468 2.542969-15.503906 7.214844-21.816406.042968-.0625.089844-.121094.132812-.183594l128.691406-181.289062c3.667969-5.097656 4.171876-11.820313 1.300782-17.40625-2.828125-5.515625-8.511719-8.9765628-14.707032-8.964844zm0 0"
              />
            </svg>
          </div>
        </div>

        <!-- filter fields -->
        <div
          v-show="isFilterVisible"
          class="field has-addons is-align-items-flex-end"
        >
          <div class="control is-expanded mr-1">
            <label for="gender">Gender</label>
            <div class="select is-fullwidth">
              <!-- populate creditcardtype dropdown menu -->
              <select v-model="selectedgender">
                <option value="">
                  Any
                </option>
                <option
                  v-for="option in genderOptions"
                  v-bind:value="option.value"
                  :key="option.ID"
                >
                  {{ option.value }}
                </option>
              </select>
            </div>
          </div>
          <div class="control is-expanded mr-1">
            <label for="creditcardtype">CreditCardType</label>
            <div class="select is-fullwidth">
              <!-- populate paymentMethod dropdown menu -->
              <select v-model="selectedpayment">
                <option value="">
                  Any
                </option>
                <option
                  v-for="option in paymentOptions"
                  v-bind:value="option.value"
                  :key="option.ID"
                >
                  {{ option.value }}
                </option>
              </select>
            </div>
          </div>
        </div>

        <!-- card grid -->
        <div class="cards">
          <!-- card -->
          <div
            class="card"
            v-for="profile in pageOfItems"
            :key="profile.UserName"
          >
            <header class="card-header">
              <p class="card-header-title">
                {{ profile.FirstName }} {{ profile.LastName }}
              </p>
            </header>
            <div class="card-content">
              <div class="content">
                <p class="info">
                  <span> UserName:</span><br />
                  {{ profile.UserName }}
                </p>
                <p class="info">
                  <span> CreditCardNumber:</span><br />
                  {{ profile.CreditCardNumber }}
                </p>
                <p class="info">
                  <span> CreditCardType:</span><br />
                  {{ profile.CreditCardType }}
                </p>
                <p class="info">
                  <span> PaymentMethod:</span><br />
                  {{ profile.PaymentMethod }}
                </p>
              </div>
            </div>
            <footer class="card-footer">
              <a
                href="#"
                class="card-footer-item btn"
                @click="showModal(profile)"
                >Details</a
              >
            </footer>

            <!-- modal component -->
            <modal v-show="isModalVisible" @close="closeModal">
              <template v-slot:body>
                <p class="info mb-1"><span>FirstName:</span> {{ FirstName }}</p>
                <p class="info mb-1"><span>LastName:</span> {{ LastName }}</p>
                <p class="info mb-1"><span>UserName: </span> {{ UserName }}</p>
                <p class="info mb-1">
                  <span>CreditCardNumber:</span> {{ CreditCardNumber }}
                </p>
                <p class="info mb-1">
                  <span>CreditCardType:</span> {{ CreditCardType }}
                </p>
                <p class="info mb-1">
                  <span>DomainName:</span> {{ DomainName }}
                </p>
                <p class="info mb-1"><span>Email:</span> {{ Email }}</p>
                <p class="info mb-1"><span>Gender:</span> {{ Gender }}</p>
                <p class="info mb-1"><span>LastLogin:</span> {{ LastLogin }}</p>
                <p class="info mb-1"><span>Latitude:</span> {{ Latitude }}</p>
                <p class="info mb-1"><span>Longitude:</span> {{ Longitude }}</p>
                <p class="info mb-1">
                  <span>MacAddress:</span> {{ MacAddress }}
                </p>
                <p class="info mb-1">
                  <span>PaymentMethod:</span> {{ PaymentMethod }}
                </p>
                <p class="info mb-1">
                  <span>PhoneNumber:</span> {{ PhoneNumber }}
                </p>
                <p class="info mb-1"><span>URL:</span> {{ URL }}</p>
              </template>
            </modal>
          </div>
        </div>
      </div>
      <div class="footer">
        <div class="is-flex is-justify-content-center">
          <jw-pagination
            :items="resultQuery"
            :pageSize="20"
            @changePage="onChangePage"
          ></jw-pagination>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import JwPagination from "jw-vue-pagination";
import modal from "./modal.vue";

export default Vue.extend({
  name: "HelloWorld",
  props: {},
  components: {
    modal,
    "jw-pagination": JwPagination,
  },
  data() {
    return {
      loading: true,
      profiles: [],
      pageOfItems: [],
      searchQuery: null,
      isFilterVisible: false,
      selectedgender: "",
      selectedpayment: "",
      isModalVisible: false,
      paymentOptions: [],
      genderOptions: [],
      FirstName: null,
      LastName: null,
      UserName: null,
      CreditCardNumber: null,
      CreditCardType: null,
      DomainName: null,
      Email: null,
      Gender: null,
      LastLogin: null,
      Latitude: null,
      Longitude: null,
      MacAddress: null,
      PaymentMethod: null,
      PhoneNumber: null,
      URL: null,
    };
  },

  // Fetches posts when the component is created.
  mounted() {
    axios
      .get(`https://api.enye.tech/v1/challenge/records`)
      .then((response) => {
        // JSON responses are automatically parsed.
        this.loading = false;
        this.profiles = response.data.records.profiles;

        // get paymentmethod options to populate dropdown
        const paymentOptionsArray = [];
        let paymentid = 0;
        for (let i = 0; i < this.profiles.length; i++) {
          if (
            paymentOptionsArray.includes(this.profiles[i].PaymentMethod) ===
            false
          ) {
            paymentOptionsArray.push(this.profiles[i].PaymentMethod);
          }
        }
        // return options object with values and unique ids
        this.paymentOptions = paymentOptionsArray.map((x) => {
          return { value: x, ID: paymentid++ };
        });

        // get paymentmethod options to populate dropdown
        const genderOptionsArray = [];
        let id = 0;
        for (let i = 0; i < this.profiles.length; i++) {
          if (genderOptionsArray.includes(this.profiles[i].Gender) === false) {
            genderOptionsArray.push(this.profiles[i].Gender);
          }
        }
        // return options object with values and unique ids
        this.genderOptions = genderOptionsArray.map((x) => {
          return { value: x, ID: id++ };
        });
      })
      .catch((e) => {
        console.log(e);
      });
  },
  methods: {
    onChangePage(pageOfItems) {
      // update page of items
      this.pageOfItems = pageOfItems;
    },
    toggleFilter() {
      this.isFilterVisible = !this.isFilterVisible;
    },
    showModal(profile) {
      this.isModalVisible = true;

      this.FirstName = profile.FirstName;
      this.LastName = profile.LastName;
      this.UserName = profile.UserName;
      this.CreditCardNumber = profile.CreditCardNumber;
      this.CreditCardType = profile.CreditCardType;
      this.DomainName = profile.DomainName;
      this.Email = profile.Email;
      this.Gender = profile.Gender;
      this.LastLogin = profile.LastLogin;
      this.Latitude = profile.Latitude;
      this.Longitude = profile.Longitude;
      this.MacAddress = profile.MacAddress;
      this.PaymentMethod = profile.PaymentMethod;
      this.PhoneNumber = profile.PhoneNumber;
      this.URL = profile.URL;
    },
    closeModal() {
      this.isModalVisible = false;
    },
  },

  computed: {
    resultQuery() {
      let newProfiles = this.profiles.slice(0, this.profiles.length);

      if (this.searchQuery) {
        newProfiles = newProfiles.filter(
          (item) => {
            return (
              this.searchQuery
                .toLowerCase()
                .split(" ")
                .every((v) =>
                  (
                    item.FirstName.toLowerCase() +
                    " " +
                    item.LastName.toLowerCase()
                  ).includes(v)
                ) ||
              this.searchQuery
                .toLowerCase()
                .split(" ")
                .every((v) =>
                  item.CreditCardNumber.toLowerCase().includes(v)
                )
            );
          }
        );
      }

      if (this.selectedgender !== "" && this.selectedpayment !== "") {
        newProfiles = newProfiles.filter(
          (item) => {
            return (
              item.Gender === this.selectedgender &&
              item.PaymentMethod === this.selectedpayment
            );
          }
        );
      }

      return newProfiles;
    },
  },
});
</script>

<style lang="scss">
.page-link {
  color: black;
  float: left;
  padding: 8px 16px;
  text-decoration: none;
  border: 1px solid #ddd;

  &:hover {
    background-color: #ddd;
  }
}

.pagination .active a {
  background-color: #49a73d;
  border: 1px solid #49a73d;
  color: #fff;
}

.info {
  font-size: 1rem;
  font-weight: 600;

  span {
    font-size: 0.85rem;
    color: gray;
  }
}

.cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  grid-auto-rows: auto;
  grid-gap: 1.5rem;

  .card {
    position: relative;

    .card-header-title {
      font-size: 1.15rem;
      color: #3f2638;
    }

    a {
      color: #49a73d;
      font-weight: 800;

      &:hover {
        color: #2c2c2c;
      }
    }
  }
}

.filter-btn {
  fill: #49a73d;

  &:hover {
    cursor: pointer;
    fill: black;
  }
}
</style>
