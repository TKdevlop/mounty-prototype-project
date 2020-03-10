<template>
  <div class="detail-container">
    <div class="info">
      <span style="font-size: 13px;">MOUNTY1450 &nbsp;</span>
      <span class="rating">&#9733; 4.6 (18 Ratings)</span>
      <h2 style="margin:10px 0px">Activity Valley View Camp</h2>
      <div>Solan, Himachal Pradesh</div>
      <div
        style="margin-top:25px"
      >Surrounded with the lush of Pine trees and snow-clad terrains of Himalayas, Solan is the perfect weekend getaway. Activity valley view camp hosts gratifying allure of breathtaking landscapes and serenity of mighty Himalayan ranges. Camping in Solan has gained popularity in recent times and not too far from the major attractions of Himachal Pradesh, Activity valley view camp is an ideal spot for you if you wish to explore more. The campsite is known for its hospitality and the delicious local cuisine is an add on. The cottages are set up on an altitude where you can get the bird's eye view of the entire valley and the cool breeze caress your face midst the vibrant chatter of mountain fauna. The campsite is surrounded by trees and you can relax away from the hustle and bustle of city life.</div>
      <ul id="point-list">
        <li v-for="item in pointList" :key="item">
          &#9733; {{item}}
          <br />
          <br />
        </li>
      </ul>
    </div>

    <div class="pricing">
      <div class="bordered-div">
        <span style="font-size:24px;font-weight:bolder">₹2156</span> / Person / Night
      </div>
      <label for="dates">Dates</label>
      <div class="dates">
        <div id="from_date">
          <input
            placeholder="Check In"
            type="text"
            style="width:100%"
            v-model="from_date"
            onfocus="(this.type='date')"
          />
        </div>
        <div id="to_date">
          <input
            placeholder="Check Out"
            type="text"
            style="width:100%"
            v-model="to_date"
            onfocus="(this.type='date')"
          />
        </div>
      </div>
      <label for>Campers</label>
      <div class="campers">
        <input type="text" style="background:#eee" disabled :value="camp_expense.campers" />
        <button @click="remove_camper" :disabled="remove_disabled">-</button>
        <button @click="add_camper">+</button>
      </div>
      <div style="padding:10px" class="add-camp">
        <h4 style="margin:0px;padding-top:3px">Select Arrangement</h4>
        <button @click="add_camp">+ CAMP</button>
      </div>
      <div class="camp" style="padding:10px;border:1px dotted black;border-radius:20px">
        <div>
          <strong>CAMP</strong>
        </div>
        <div>
          <strong>CAMPERS</strong>
        </div>
      </div>
      <div class="camps">
        <div v-for="camp in camp_expense.camps" :key="camp.key" class="camp">
          <div>
            <div>camp {{camp.key + 1}}</div>
            <strong style="font-size:12px">₹{{camp.price}}</strong>
          </div>
          <div>
            <strong>{{camp.campers}}</strong>
          </div>
          <div>
            <strong @click="remove_camp(camp.key, camp.campers)" style="cursor:pointer">&#215;</strong>
          </div>
        </div>
      </div>
      <div style="text-align:center" class="total">
        Total : ₹
        <strong>{{ camp_expense.total_expense }}</strong>
      </div>
      <button @click="showData" id="book">BOOK ONLINE</button>
    </div>
  </div>
</template>
<script>
function get_date_day_diff(from_date, to_date) {
  if (!from_date) return null;
  const oneDay = 24 * 60 * 60 * 1000; // hours*minutes*seconds*milliseconds
  const firstDate = new Date(from_date);
  const secondDate = new Date(to_date);
  return Math.round(Math.abs((firstDate - secondDate) / oneDay));
}
export default {
  name: "CampDetails",
  data() {
    return {
      from_date: "",
      to_date: "",
      no_of_day: 1,
      camp_expense: {
        max_campers_per_camp: 3,
        min_campers: 2,
        price_per_night: 2156,
        campers: 3,
        camps: [
          {
            //hardcoded first element for default
            key: 0,
            price: 3 * 2156,
            campers: 3
          }
        ],
        total_expense: 3 * 2156
      },
      pointList: [
        "Approx. 2 acres of a property area",
        "The property is surrounded by hills and covered with trees",
        "Parking space is available in the property area",
        "Attached washrooms are available in the property",
        "Valley view is clearly visible from the property area"
      ]
    };
  },
  computed: {
    remove_disabled() {
      if (this.camp_expense.campers <= this.camp_expense.min_campers) {
        return true;
      }
      return false;
    }
  },
  watch: {
    "camp_expense.campers": function() {
      this.calculate_total_expense();
    }
  },
  methods: {
    add_camp() {
      const {
        camp_expense: { max_campers_per_camp, price_per_night, camps }
      } = this;
      this.camp_expense.campers += max_campers_per_camp;
      let number_of_days = 1;
      const days = get_date_day_diff(this.from_date, this.to_date);
      if (days !== null) {
        number_of_days = days;
      }
      let price =
        max_campers_per_camp *
        number_of_days *
        price_per_night *
        number_of_days;
      console.log(max_campers_per_camp, number_of_days, price_per_night);
      camps.push({
        price,
        key: camps.length,
        campers: max_campers_per_camp
      });
      this.camp_expense.total_expense += price;
    },
    remove_camp(key, campers) {
      this.camp_expense.campers -= campers;
      // map part to make sure the key is unique
      const filter_camps = this.camp_expense.camps
        .filter(item => item.key !== key)
        .map((item, i) => ({ ...item, key: i }));
      this.camp_expense.camps = filter_camps;
    },
    calculate_total_expense() {
      const {
        camp_expense: { max_campers_per_camp, campers, price_per_night }
      } = this;
      let number_of_days = 1;
      const days = get_date_day_diff(this.from_date, this.to_date);
      if (days !== null) {
        number_of_days = days;
      }
      let total_camps = null;
      const remainder = campers % max_campers_per_camp;
      total_camps = parseInt(campers / max_campers_per_camp);
      const update_camps = [];
      let total = 0;
      for (let i = 0; i < total_camps; i++) {
        let price =
          max_campers_per_camp *
          number_of_days *
          price_per_night *
          number_of_days;
        update_camps.push({
          price,
          key: i,
          campers: max_campers_per_camp
        });
        total += price;
      }
      if (remainder > 0) {
        let price =
          remainder * number_of_days * price_per_night * number_of_days;
        update_camps.push({
          key: update_camps.length,
          price,
          campers: remainder
        });
        total += price;
      }
      this.camp_expense.camps = update_camps;
      this.camp_expense.total_expense = total;
    },
    remove_camper() {
      this.camp_expense.campers -= 1;
    },
    add_camper() {
      this.camp_expense.campers += 1;
    },
    showData() {
      // console.log(get_date_day_diff(this.from_date, this.to_date));
      // console.log(this.camp_expense);
      alert("THANKS FOR BUYING THE CAMP TRIP");
    }
  }
};
</script>
<style scoped>
#book {
  margin: auto;
  display: block;
  width: 100%;
  margin-top: 10px;
  padding: 10px;
  border: 0px;
  color: #fff;
  background: orangered;
}
button {
  cursor: pointer;
}
.rating {
  background: #eee;
  font-size: 11px;
  border-radius: 30px;
  color: #c51162;
  padding: 5px;
}
#point-list {
  list-style-type: none;
  padding: 0px;
}
.detail-container {
  max-width: 90%;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  grid-gap: 20px;
  margin-top: 50px;
}
.detail-container {
  text-align: left;
}
.dates {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;
}
.campers {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
}
.add-camp {
  display: grid;
  grid-template-columns: 2fr 1fr;
}
.camp {
  display: grid;
  grid-template-columns: 2fr 2fr 1fr;
  padding: 5px;
  align-items: center;
  border-bottom: 1px solid black;
  border-radius: 20px;
}
.pricing > * {
  margin-bottom: 20px;
}
</style>