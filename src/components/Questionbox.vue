<template>
  <div class="qb">
    <div class="qb__container">
      <div class="qb__numbers">
        <span
          v-for="(question, ind) in allQuestions"
          :key="question.question"
          :class="[
            question.attempt === true ? 'selected' : '',
            index === ind ? 'boxsh' : '',
          ]"
          @click="changeIndex(ind)"
          >{{ ind + 1 }}</span
        >
      </div>
      <div class="qb__question">{{ el.question }}</div>
      <b-list-group>
        <b-list-group-item
          v-for="option in options"
          :active="el.picked === option && !isSubmitted"
          :key="option"
          @click="!isSubmitted && updateQuestion(option)"
          :class="[
            isSubmitted && el.picked === option ? 'opt_selected_wrong' : '',
            isSubmitted && el.correct_answer === option ? 'opt_selected' : '',
          ]"
          >{{ option }}</b-list-group-item
        >
      </b-list-group>
      <div class="qb__buttons">
        <b-button
          size="sm"
          variant="success"
          v-if="!isSubmitted"
          @click="submit"
          >Submit</b-button
        >
        <div>
          <b-button
            size="sm"
            style="margin-right: 10px"
            :disabled="index === 0"
            @click="prev"
            variant="info"
            >Prev</b-button
          >
          <b-button
            size="sm"
            :disabled="index === 9"
            @click="next"
            variant="info"
            >Next</b-button
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Questionbox",
  props: [
    "el",
    "index",
    "next",
    "prev",
    "updateQuestion",
    "submit",
    "allQuestions",
    "changeIndex",
    "isSubmitted",
  ],
  computed: {
    options() {
      let opt = [...this.el.incorrect_answers, this.el.correct_answer];
      return opt;
    },
  },
};
</script>

<style scoped>
.qb {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 30px;
}
.qb__container {
  padding: 40px;
  width: 500px;
  box-shadow: 5px 5px 8px 10px #888888;
}
.qb__question {
  margin-bottom: 10px;
}
.qb__buttons {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}
.qb__selected {
  background-color: bisque;
}
.qb__numbers {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  margin-bottom: 20px;
}
.qb__numbers > span {
  border: 1px solid lightgray;
  width: 25px;
  padding: 2px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  cursor: pointer;
}
.selected {
  background-color: #427bff;
}
.boxsh {
  box-shadow: 4px 0px 6px #888888;
}
.opt_selected_wrong {
  background-color: lightcoral;
}
.opt_selected {
  background-color: lightgreen;
}
</style>