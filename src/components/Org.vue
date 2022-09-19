<template>
  <div id="org" @click.self="locationFilter = false">
    <div class="tabs">
      <div class="d-flex">
        <div class="tab bg-white" @click="locationFilter = true">
          <span>Location</span>
          <span class="badge-count" v-show="getSelected.length > 0">{{
            getSelected.length
          }}</span>
        </div>
        <div class="tab active" @click="advanceFilter = true">
          <span>Advanced filters</span>
        </div>
      </div>
      <div class="search-box" v-show="locationFilter">
        <section>
          <div class="d-flex justify-content-between align-items-center title">
            <span>Country</span>
            <img
              src="https://app.netzeroinsights.com/images/icons/1.Filter_Green.png"
              alt=""
            />
          </div>
          <div class="search">
            <input
              class="input"
              type="text"
              placeholder="Search by country"
              v-model="searchQuery"
            />
          </div>
          <ul class="list-unstyled mb-0">
            <li class="listing" v-for="role in locationQuery" :key="role.id">
              <input
                :id="role.name"
                class="form-check-input"
                type="checkbox"
                v-model="selectedLocation.location"
                :value="role"
              />
              <label class="form-check-label" :for="role.name">{{
                role.name
              }}</label>
            </li>
          </ul>
        </section>
        <section>
          <div class="d-flex justify-content-between align-items-center title">
            <span>Region</span>
            <img
              src="https://app.netzeroinsights.com/images/icons/1.Filter_Green.png"
              alt=""
            />
          </div>
          <div class="search">
            <input
              class="input"
              type="text"
              placeholder="Search by country"
              v-model="searchRegion"
            />
          </div>
          <ul class="list-unstyled mb-0">
            <li class="listing" v-for="(item, index) in rgnQuery" :key="index">
              <input
                :id="index"
                class="form-check-input"
                type="checkbox"
                v-model="slectedReligion.religion"
                :value="item"
              />
              <label class="form-check-label" :for="index">{{ item }}</label>
            </li>
          </ul>
        </section>
      </div>
    </div>

    <!-- Advance filter start -->
    <transition name="advance-filter">
      <div class="advance-filter" v-show="advanceFilter">
        <div class="d-flex">
          <div class="col-2">
            <div class="active">Overview</div>
            <div>Activity Sectord</div>
            <div>impact matrics</div>
            <div>funding rounds</div>
            <div>patents</div>
            <div>wildcard match</div>
            <div>custom filters</div>
          </div>
          <div class="col-10 position-relative">
            <div class="p-40">
              <div class="title">
                <span>LOCATION</span>
              </div>
              <div class="search">
                <input
                  class="input"
                  type="text"
                  placeholder="Type to search"
                  v-model="searchQuery"
                />
              </div>
              <div class="mt-30">
                <div class="title">
                  <span>Founded year</span>
                </div>
                <div class="d-flex align-items-center">
                  <div class="search w-100p">
                    <input
                      class="input"
                      type="number"
                      placeholder="2010"
                      v-model="from"
                    />
                  </div>
                  <span class="mx-30">to</span>
                  <div class="search w-100p">
                    <input
                      class="input"
                      type="number"
                      placeholder="2022"
                      v-model="to"
                    />
                  </div>
                </div>
              </div>
              <div class="mt-30">
                <div class="title">
                  <span>Founded year</span>
                </div>
                <ul class="list-unstyled mb-0" style="columns: auto 3">
                  <li
                    class="listing"
                    v-for="(item, index) in year"
                    :key="index"
                  >
                    <input
                      :id="index"
                      class="form-check-input"
                      type="checkbox"
                      v-model="slectedyear.year"
                      :value="item"
                    />
                    <label class="form-check-label" :for="index">{{
                      item
                    }}</label>
                  </li>
                </ul>
              </div>

              <div class="mt-30">
                <div class="title">
                  <span>Stage</span>
                </div>
                <ul class="list-unstyled mb-0" style="columns: 4">
                  <li
                    class="listing"
                    v-for="(item, index) in rgnQuery"
                    :key="index"
                  >
                    <input
                      :id="index"
                      class="form-check-input"
                      type="checkbox"
                      v-model="slectedReligion.religion"
                      :value="item"
                    />
                    <label class="form-check-label" :for="index">{{
                      item
                    }}</label>
                  </li>
                  <li
                    class="listing"
                    v-for="(item, index) in rgnQuery"
                    :key="index"
                  >
                    <input
                      :id="index"
                      class="form-check-input"
                      type="checkbox"
                      v-model="slectedReligion.religion"
                      :value="item"
                    />
                    <label class="form-check-label" :for="index">{{
                      item
                    }}</label>
                  </li>
                </ul>
              </div>
            </div>
            <div class="button-section border-top bg-white">
              <div class="px-30">
                <ul class="list-inline mb-0 py-15">
                  <li class="list-inline-item" v-show="from && !to">
                    From {{ from }}
                    <span class="remove-filter" @click="from = ''">+</span>
                    <span class="include-exclude">-</span>
                  </li>
                  <li class="list-inline-item" v-show="from && to">
                    {{ from }} - {{ to }}
                    <span
                      class="remove-filter"
                      @click="
                        from = '';
                        to = '';
                      "
                      >+</span
                    >
                    <span class="include-exclude">-</span>
                  </li>
                  <li class="list-inline-item" v-show="!from && to">
                    To {{ to }}
                    <span class="remove-filter" @click="to = ''">+</span>
                    <span class="include-exclude">-</span>
                  </li>
                  <li
                    class="list-inline-item"
                    v-for="(item, index) in slectedyear.year"
                    :key="index"
                  >
                    {{ item }}
                    <span class="remove-filter">+</span>
                    <span class="include-exclude">-</span>
                  </li>
                </ul>
              </div>
              <div
                class="px-30 py-10 d-flex border-top justify-content-between align-items-center"
              >
                <span>Results</span>
                <div class="d-flex align-items-center">
                  <button class="button fill">Apply</button>
                  <button class="button">clear all</button>
                  <span role="button" @click="advanceFilter = false"
                    >Cancel</span
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </transition>

    <!-- Advance filter end -->
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  data() {
    return {
      locationFilter: false,
      advanceFilter: false,
      searchQuery: "",
      searchRegion: "",
      from: "",
      to: "",
      slectedyear: {
        year: [],
      },
      year: [
        "1 - 10",
        "11 - 50",
        "51 - 100",
        "101 - 200",
        "201 - 500",
        "501 - 1000",
        "1001 - 5000",
        "5001 - 10000",
        "10000 +",
      ],
      slectedReligion: {
        religion: [],
      },
      religion: [
        "Arianism",
        "Christadelphians",
        "Christian",
        " Gnosticism",
        "Identity",
        " Science",
        "Christian",
        "Universalism",
        "Iglesia ni Cristo",
        "Ebionites",
        "Jehovah's Witnesses",
        "Jesuism",
        "Latter Day ",
        "Millerites",
        "Nontrinitarianism",
        "Messianic Judaism",
        "Marcionism",
        "Rastafarianism",
        "Spiritual Baptists",
        "Swedenborgianism",
        "The Aquarian Church",
        "Unification Church",
        "Unitarianism",
      ],
      selectedLocation: {
        location: [],
      },
      location: [
        { name: "Afghanistan", code: "AF" },
        { name: "Åland Islands", code: "AX" },
        { name: "Albania", code: "AL" },
        { name: "Algeria", code: "DZ" },
        { name: "American Samoa", code: "AS" },
        { name: "AndorrA", code: "AD" },
        { name: "Angola", code: "AO" },
        { name: "Anguilla", code: "AI" },
        { name: "Antarctica", code: "AQ" },
        { name: "Antigua and Barbuda", code: "AG" },
        { name: "Argentina", code: "AR" },
        { name: "Armenia", code: "AM" },
        { name: "Aruba", code: "AW" },
        { name: "Australia", code: "AU" },
        { name: "Austria", code: "AT" },
        { name: "Azerbaijan", code: "AZ" },
        { name: "Bahamas", code: "BS" },
        { name: "Bahrain", code: "BH" },
        { name: "Bangladesh", code: "BD" },
        { name: "Barbados", code: "BB" },
        { name: "Belarus", code: "BY" },
        { name: "Belgium", code: "BE" },
        { name: "Belize", code: "BZ" },
        { name: "Benin", code: "BJ" },
        { name: "Bermuda", code: "BM" },
        { name: "Bhutan", code: "BT" },
        { name: "Bolivia", code: "BO" },
        { name: "Bosnia and Herzegovina", code: "BA" },
        { name: "Botswana", code: "BW" },
        { name: "Bouvet Island", code: "BV" },
        { name: "Brazil", code: "BR" },
        { name: "British Indian Ocean Territory", code: "IO" },
        { name: "Brunei Darussalam", code: "BN" },
        { name: "Bulgaria", code: "BG" },
        { name: "Burkina Faso", code: "BF" },
        { name: "Burundi", code: "BI" },
        { name: "Cambodia", code: "KH" },
        { name: "Cameroon", code: "CM" },
        { name: "Canada", code: "CA" },
        { name: "Cape Verde", code: "CV" },
        { name: "Cayman Islands", code: "KY" },
        { name: "Central African Republic", code: "CF" },
        { name: "Chad", code: "TD" },
        { name: "Chile", code: "CL" },
        { name: "China", code: "CN" },
        { name: "Christmas Island", code: "CX" },
        { name: "Cocos (Keeling) Islands", code: "CC" },
        { name: "Colombia", code: "CO" },
        { name: "Comoros", code: "KM" },
        { name: "Congo", code: "CG" },
        { name: "Congo, The Democratic Republic of the", code: "CD" },
        { name: "Cook Islands", code: "CK" },
        { name: "Costa Rica", code: "CR" },
        { name: "Cote D'Ivoire", code: "CI" },
        { name: "Croatia", code: "HR" },
        { name: "Cuba", code: "CU" },
        { name: "Cyprus", code: "CY" },
        { name: "Czech Republic", code: "CZ" },
        { name: "Denmark", code: "DK" },
        { name: "Djibouti", code: "DJ" },
        { name: "Dominica", code: "DM" },
        { name: "Dominican Republic", code: "DO" },
        { name: "Ecuador", code: "EC" },
        { name: "Egypt", code: "EG" },
        { name: "El Salvador", code: "SV" },
        { name: "Equatorial Guinea", code: "GQ" },
        { name: "Eritrea", code: "ER" },
        { name: "Estonia", code: "EE" },
        { name: "Ethiopia", code: "ET" },
        { name: "Falkland Islands (Malvinas)", code: "FK" },
        { name: "Faroe Islands", code: "FO" },
        { name: "Fiji", code: "FJ" },
        { name: "Finland", code: "FI" },
        { name: "France", code: "FR" },
        { name: "French Guiana", code: "GF" },
        { name: "French Polynesia", code: "PF" },
        { name: "French Southern Territories", code: "TF" },
        { name: "Gabon", code: "GA" },
        { name: "Gambia", code: "GM" },
        { name: "Georgia", code: "GE" },
        { name: "Germany", code: "DE" },
        { name: "Ghana", code: "GH" },
        { name: "Gibraltar", code: "GI" },
        { name: "Greece", code: "GR" },
        { name: "Greenland", code: "GL" },
        { name: "Grenada", code: "GD" },
        { name: "Guadeloupe", code: "GP" },
        { name: "Guam", code: "GU" },
        { name: "Guatemala", code: "GT" },
        { name: "Guernsey", code: "GG" },
        { name: "Guinea", code: "GN" },
        { name: "Guinea-Bissau", code: "GW" },
        { name: "Guyana", code: "GY" },
        { name: "Haiti", code: "HT" },
        { name: "Heard Island and Mcdonald Islands", code: "HM" },
        { name: "Holy See (Vatican City State)", code: "VA" },
        { name: "Honduras", code: "HN" },
        { name: "Hong Kong", code: "HK" },
        { name: "Hungary", code: "HU" },
        { name: "Iceland", code: "IS" },
        { name: "India", code: "IN" },
        { name: "Indonesia", code: "ID" },
        { name: "Iran, Islamic Republic Of", code: "IR" },
        { name: "Iraq", code: "IQ" },
        { name: "Ireland", code: "IE" },
        { name: "Isle of Man", code: "IM" },
        { name: "Israel", code: "IL" },
        { name: "Italy", code: "IT" },
        { name: "Jamaica", code: "JM" },
        { name: "Japan", code: "JP" },
        { name: "Jersey", code: "JE" },
        { name: "Jordan", code: "JO" },
        { name: "Kazakhstan", code: "KZ" },
        { name: "Kenya", code: "KE" },
        { name: "Kiribati", code: "KI" },
        { name: "Korea, Democratic People'S Republic of", code: "KP" },
        { name: "Korea, Republic of", code: "KR" },
        { name: "Kuwait", code: "KW" },
        { name: "Kyrgyzstan", code: "KG" },
        { name: "Lao People'S Democratic Republic", code: "LA" },
        { name: "Latvia", code: "LV" },
        { name: "Lebanon", code: "LB" },
        { name: "Lesotho", code: "LS" },
        { name: "Liberia", code: "LR" },
        { name: "Libyan Arab Jamahiriya", code: "LY" },
        { name: "Liechtenstein", code: "LI" },
        { name: "Lithuania", code: "LT" },
        { name: "Luxembourg", code: "LU" },
        { name: "Macao", code: "MO" },
        { name: "Macedonia, The Former Yugoslav Republic of", code: "MK" },
        { name: "Madagascar", code: "MG" },
        { name: "Malawi", code: "MW" },
        { name: "Malaysia", code: "MY" },
        { name: "Maldives", code: "MV" },
        { name: "Mali", code: "ML" },
        { name: "Malta", code: "MT" },
        { name: "Marshall Islands", code: "MH" },
        { name: "Martinique", code: "MQ" },
        { name: "Mauritania", code: "MR" },
        { name: "Mauritius", code: "MU" },
        { name: "Mayotte", code: "YT" },
        { name: "Mexico", code: "MX" },
        { name: "Micronesia, Federated States of", code: "FM" },
        { name: "Moldova, Republic of", code: "MD" },
        { name: "Monaco", code: "MC" },
        { name: "Mongolia", code: "MN" },
        { name: "Montserrat", code: "MS" },
        { name: "Morocco", code: "MA" },
        { name: "Mozambique", code: "MZ" },
        { name: "Myanmar", code: "MM" },
        { name: "Namibia", code: "NA" },
        { name: "Nauru", code: "NR" },
        { name: "Nepal", code: "NP" },
        { name: "Netherlands", code: "NL" },
        { name: "Netherlands Antilles", code: "AN" },
        { name: "New Caledonia", code: "NC" },
        { name: "New Zealand", code: "NZ" },
        { name: "Nicaragua", code: "NI" },
        { name: "Niger", code: "NE" },
        { name: "Nigeria", code: "NG" },
        { name: "Niue", code: "NU" },
        { name: "Norfolk Island", code: "NF" },
        { name: "Northern Mariana Islands", code: "MP" },
        { name: "Norway", code: "NO" },
        { name: "Oman", code: "OM" },
        { name: "Pakistan", code: "PK" },
        { name: "Palau", code: "PW" },
        { name: "Palestinian Territory, Occupied", code: "PS" },
        { name: "Panama", code: "PA" },
        { name: "Papua New Guinea", code: "PG" },
        { name: "Paraguay", code: "PY" },
        { name: "Peru", code: "PE" },
        { name: "Philippines", code: "PH" },
        { name: "Pitcairn", code: "PN" },
        { name: "Poland", code: "PL" },
        { name: "Portugal", code: "PT" },
        { name: "Puerto Rico", code: "PR" },
        { name: "Qatar", code: "QA" },
        { name: "Reunion", code: "RE" },
        { name: "Romania", code: "RO" },
        { name: "Russian Federation", code: "RU" },
        { name: "RWANDA", code: "RW" },
        { name: "Saint Helena", code: "SH" },
        { name: "Saint Kitts and Nevis", code: "KN" },
        { name: "Saint Lucia", code: "LC" },
        { name: "Saint Pierre and Miquelon", code: "PM" },
        { name: "Saint Vincent and the Grenadines", code: "VC" },
        { name: "Samoa", code: "WS" },
        { name: "San Marino", code: "SM" },
        { name: "Sao Tome and Principe", code: "ST" },
        { name: "Saudi Arabia", code: "SA" },
        { name: "Senegal", code: "SN" },
        { name: "Serbia and Montenegro", code: "CS" },
        { name: "Seychelles", code: "SC" },
        { name: "Sierra Leone", code: "SL" },
        { name: "Singapore", code: "SG" },
        { name: "Slovakia", code: "SK" },
        { name: "Slovenia", code: "SI" },
        { name: "Solomon Islands", code: "SB" },
        { name: "Somalia", code: "SO" },
        { name: "South Africa", code: "ZA" },
        { name: "South Georgia and the South Sandwich Islands", code: "GS" },
        { name: "Spain", code: "ES" },
        { name: "Sri Lanka", code: "LK" },
        { name: "Sudan", code: "SD" },
        { name: "Suriname", code: "SR" },
        { name: "Svalbard and Jan Mayen", code: "SJ" },
        { name: "Swaziland", code: "SZ" },
        { name: "Sweden", code: "SE" },
        { name: "Switzerland", code: "CH" },
        { name: "Syrian Arab Republic", code: "SY" },
        { name: "Taiwan, Province of China", code: "TW" },
        { name: "Tajikistan", code: "TJ" },
        { name: "Tanzania, United Republic of", code: "TZ" },
        { name: "Thailand", code: "TH" },
        { name: "Timor-Leste", code: "TL" },
        { name: "Togo", code: "TG" },
        { name: "Tokelau", code: "TK" },
        { name: "Tonga", code: "TO" },
        { name: "Trinidad and Tobago", code: "TT" },
        { name: "Tunisia", code: "TN" },
        { name: "Turkey", code: "TR" },
        { name: "Turkmenistan", code: "TM" },
        { name: "Turks and Caicos Islands", code: "TC" },
        { name: "Tuvalu", code: "TV" },
        { name: "Uganda", code: "UG" },
        { name: "Ukraine", code: "UA" },
        { name: "United Arab Emirates", code: "AE" },
        { name: "United Kingdom", code: "GB" },
        { name: "United States", code: "US" },
        { name: "United States Minor Outlying Islands", code: "UM" },
        { name: "Uruguay", code: "UY" },
        { name: "Uzbekistan", code: "UZ" },
        { name: "Vanuatu", code: "VU" },
        { name: "Venezuela", code: "VE" },
        { name: "Viet Nam", code: "VN" },
        { name: "Virgin Islands, British", code: "VG" },
        { name: "Virgin Islands, U.S.", code: "VI" },
        { name: "Wallis and Futuna", code: "WF" },
        { name: "Western Sahara", code: "EH" },
        { name: "Yemen", code: "YE" },
        { name: "Zambia", code: "ZM" },
        { name: "Zimbabwe", code: "ZW" },
      ],
    };
  },
  methods: {},
  computed: {
    locationQuery() {
      if (this.searchQuery) {
        return this.location.filter((item: any) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => item.name.toLowerCase().includes(v));
        });
      } else {
        return this.location?.splice(0, 5);
      }
    },
    rgnQuery() {
      if (this.searchRegion) {
        return this.religion.filter((item) => {
          return this.searchRegion
            .toLowerCase()
            .split(" ")
            .every((v) => item.toLowerCase().includes(v));
        });
      } else {
        return this.religion.splice(0, 5);
      }
    },
    getSelected() {
      let loc = this.selectedLocation.location;
      let reg = this.slectedReligion?.religion;
      if (loc || reg) {
        return loc.concat(reg);
      }
    },
  },
});
</script>

<style lang="scss" scoped>
#org {
  padding: 3.125rem;
  height: 100%;
  .tabs {
    position: relative;
    .badge-count {
      position: absolute;
      bottom: 100%;
      left: 100%;
      background: #5abf6e;
      border-radius: 13px;
      width: 20px;
      height: 20px;
      display: flex;
      align-items: center;
      justify-content: center;
      transform: translate(-12px, 10px);
      color: #fff;
    }
    .search-box {
      position: absolute;
      top: 50px;
      left: 5px;
      width: 250px;
      background: #fff;
      border: 1px solid hsla(0, 0%, 44%, 0.12) !important;
      border-radius: 1rem;
      section {
        .title {
          font-size: 0.9375rem;
          font-weight: 600;
          padding: 0.3rem 0.75rem;
        }
        img {
          width: 0.75rem;
          height: 0.75rem;
        }
        .search {
          padding: 0.3125rem 0.625rem 0.625rem 0.625rem;
          input {
            appearance: none;
            background-color: #fff;
            border: 1px solid hsla(0, 0%, 44%, 0.12);
            border-radius: 1rem;
            height: 2rem;
            padding: 0 1rem;
            color: #232426;
            width: 100%;
          }
        }
        ul {
          height: 170px;
          overflow: auto;
        }
        .listing {
          padding: 6.4px 12px;
          font-size: 14px;
          &:hover {
            background: #c4ffcf;
          }
        }
      }
    }
  }
  .tab {
    margin: 0 5px;
    padding: 7px 13px;
    border: 1px solid #d3d3d3;
    border-radius: 2rem;
    line-height: 1.5;
    position: relative;
    cursor: pointer;
    color: #232426;
    font-family: Poppins, Helvetica Neue, Helvetica, Arial, sans-serif;
    font-size: 0.875rem;
    font-weight: 300;
    z-index: 3;
    &.active {
      background-color: #5abf6e;
      border-color: #5abf6e;
      color: #fff;
      font-weight: 400;
      padding: 7px 15px;
      letter-spacing: 1px;
      transition: all 0.3s ease;
      &:hover {
        color: #5abf6e;
        background: #fff;
        border-color: #d3d3d3;
      }
    }
  }
}
.advance-filter {
  font-size: 0.875rem;
  position: fixed;
  top: 0%;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: 999;
  .col-2 {
    background: #f8fcfc;
    min-height: 100vh;
    padding: 1.5625rem 0.9375rem;
    border-right: 1px solid hsla(0, 0%, 44%, 0.12);
    div {
      padding: 15px 5px;
      text-transform: uppercase;
      cursor: pointer;
      &.active {
        font-weight: 600;
        color: #7bd08c;
      }
    }
  }
  .col-10 {
    background: #fff;
    min-height: 100vh;
  }
}
.advance-filter-enter-active,
.advance-filter-leave-active {
  transition: all 0.5s ease;
}

.advance-filter-enter {
  transform: translateY(100%);
}

.advance-filter-enter-to {
  transform: translateY(0);
}

.advance-filter-leave-to {
  transform: translateY(100%);
}
</style>
