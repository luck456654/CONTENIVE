<template>
  <body>
    <div class="modalWindow" ref="modalWindow" id="777">
      <div class="modalWindow__form">
        <div class="modalWindow__title">Choose a city</div>
        <div class="modalWindow__desk">
          To find city start typing and pick one from the suggestions
        </div>
        <input
          class="modalWindow__input"
          placeholder="Search city"
          ref="addCityInput"
        />
        <div class="modalWindow__buttons">
          <button class="modalWindow__button">CLEAR</button>
          <div class="modalWindow__add">
            <button class="modalWindow__button">CANCEL</button>
            <button @click="addCity" class="modalWindow__button">ADD</button>
          </div>
        </div>
      </div>
    </div>
    <h1 class="title">World Weather</h1>
    <h2 class="desck">Watch weather in your current location</h2>
    <form class="form">
      <div class="form__title">{{MoscowData.data.name}},{{MoscowData.data.sys.country}}</div>
      <p class="form__desk">Your current location</p>
      <ul class="form__ul">
        <li class="form__li">
          <div>Weather</div>
          <div>{{MoscowData.data.weather[0].description}}</div>
        </li>
        <li class="form__li">
          <div>Temperature</div>
          <div>{{MoscowData.data.main.temp_max}}</div>
        </li>
        <li class="form__li">
          <div>Humidity</div>
          <div>{{MoscowData.data.main.humidity}}</div>
        </li>
        <li>
          <div class="form__time">Время</div>
        </li>
        <li>
          <div class="form__button">RELOAD</div>
        </li>
      </ul>
    </form>
    <button class="button-add" @click="showModal">ADD CITY</button>
    <div class="form__AddCity">
    <form v-for="item in dataCity"
              :key="item.id"
               class="form formAddCity" >
      <div class="form__title">{{item.data.name}},{{item.data.sys.country}}</div>
      <p class="form__desk">Your current location</p>
      <ul class="form__ul formAddCity__ul">
        <li class="form__li">
          <div>Weather</div>
          <div>{{item.data.weather[0].description}}</div>
        </li>
        <li class="form__li">
          <div>Temperature</div>
          <div>{{item.data.main.temp_max}}</div>
        </li>
        <li class="form__li">
          <div>Humidity</div>
          <div>{{item.data.main.humidity}}</div>
        </li>
        <li>
          <div class="form__time">Время</div>
        </li>
        <li class="form__li formAddCity__li">
          <div class="form__button">REMOVE</div>
          <div class="form__button">RELOAD</div>
        </li>
      </ul>
    </form>
    </div>
    <svg
      class="button__svd-add"
      viewBox="0 0 76 76"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <g filter="url(#filter0_ddd_20_7)">
        <path
          d="M10 37C10 21.536 22.536 9 38 9V9C53.464 9 66 21.536 66 37V37C66 52.464 53.464 65 38 65V65C22.536 65 10 52.464 10 37V37Z"
          fill="#9B51E0"
        />
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M45 38H39V44H37V38H31V36H37V30H39V36H45V38Z"
          fill="white"
          fill-opacity="0.87"
        />
      </g>
      <defs>
        <filter
          id="filter0_ddd_20_7"
          x="0"
          y="0"
          width="76"
          height="76"
          filterUnits="userSpaceOnUse"
          color-interpolation-filters="sRGB"
        >
          <feFlood flood-opacity="0" result="BackgroundImageFix" />
          <feColorMatrix
            in="SourceAlpha"
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
            result="hardAlpha"
          />
          <feOffset dy="2" />
          <feGaussianBlur stdDeviation="2" />
          <feColorMatrix
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.2 0"
          />
          <feBlend
            mode="normal"
            in2="BackgroundImageFix"
            result="effect1_dropShadow_20_7"
          />
          <feColorMatrix
            in="SourceAlpha"
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
            result="hardAlpha"
          />
          <feOffset dy="1" />
          <feGaussianBlur stdDeviation="5" />
          <feColorMatrix
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.12 0"
          />
          <feBlend
            mode="normal"
            in2="effect1_dropShadow_20_7"
            result="effect2_dropShadow_20_7"
          />
          <feColorMatrix
            in="SourceAlpha"
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 127 0"
            result="hardAlpha"
          />
          <feOffset dy="4" />
          <feGaussianBlur stdDeviation="2.5" />
          <feColorMatrix
            type="matrix"
            values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0.14 0"
          />
          <feBlend
            mode="normal"
            in2="effect2_dropShadow_20_7"
            result="effect3_dropShadow_20_7"
          />
          <feBlend
            mode="normal"
            in="SourceGraphic"
            in2="effect3_dropShadow_20_7"
            result="shape"
          />
        </filter>
      </defs>
    </svg>
    
  </body>
</template>

<script>
import axios from "axios";
import "@/components/css/style.min.css";

/*const BASEURL =
  "https://api.openweathermap.org/data/2.5/weather?q=London,uk&APPID=769acfb2b423d6376361ff6032d02022";*/
export default {
  name: "ProductsList",
  data() {
    return {
      data: [],
      currentCity: "",
      MoscowData:'',
      city:'',
      dataCity:[],
    };
  },
  methods: {
    showModal() {
      this.$refs.modalWindow.style.display = "flex";
    },
    addCity() {
      this.city=this.$refs.addCityInput.value
      localStorage.setItem("city", this.$refs.addCityInput.value);
     /* alert(this.$refs.addCityInput.value);*/
      this.loadData(this.$refs.addCityInput.value);
      this.$refs.modalWindow.style.display = "none";
    },
    loadData(city) {
      localStorage.getItem("city");
      axios
        .post(
          "https://api.openweathermap.org/data/2.5/weather?q=" +
            city +
            "+&APPID=769acfb2b423d6376361ff6032d02022"
        )
        .then((response) => {
          if (city=='Moscow,RU'){
            this.MoscowData=response
          }
         else{
           alert('this.city')
            this.dataCity.push(response)
            }
        });
    },
  },
  created() {
    this.loadData("Moscow,RU");
  },
};
</script>









