<template>
  <div class="home">
    <span v-if="isSubmitted"
      ><b>Score is: {{ count }}</b
      ><br />
      <span class="home_ans_link">Check answers below</span></span
    >
    <Questionbox
      v-if="allQuestions.length > 0"
      :el="allQuestions[index]"
      :allQuestions="allQuestions"
      :index="index"
      :next="next"
      :prev="prev"
      :submit="submit"
      :updateQuestion="updateQuestion"
      :changeIndex="changeIndex"
      :isSubmitted="isSubmitted"
    />
  </div>
</template>

<script>
// @ is an alias to /src

import axios from "axios";
import Questionbox from "../components/Questionbox";

export default {
  name: "Home",
  components: {
    Questionbox,
  },
  data() {
    return {
      allQuestions: [],
      index: 0,
      count: 0,
      isSubmitted: false,
    };
  },
  methods: {
    next() {
      this.index++;
    },
    prev() {
      this.index--;
    },
    updateQuestion(val) {
      let data = [...this.allQuestions];
      data = data.map((el, index) => {
        if (index === this.index) {
          return { ...el, attempt: true, picked: val };
        }
        return el;
      });
      this.allQuestions = data;
    },
    submit() {
      let cnt = 0;
      this.allQuestions.map((el) => {
        if (el.picked === el.correct_answer) {
          console.log("y");
          cnt++;
        }
      });
      this.count = cnt;
      this.isSubmitted = true;
    },
    changeIndex(ind) {
      this.index = ind;
    },
  },
  mounted: function () {
    axios
      .get("https://opentdb.com/api.php?amount=10&category=19&type=multiple")
      .then((res) => {
        let data = res.data.results.map((el) => {
          return { ...el, attempt: false, picked: "" };
        });
        this.allQuestions = data;
      })
      .catch((err) => console.log(err));
  },
};
</script>
<style scoped>
.home {
  margin: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.home_ans_link {
  font-size: 12px;
}
</style>
