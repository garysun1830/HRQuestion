<template>
  <article class="panel new-panel" v-if="visible">
    <textarea
      :class="'textarea ' + new_question_class"
      placeholder="Question:"
      v-model="new_question"
    ></textarea>
    <textarea
      :class="'textarea ' + new_answer_class"
      placeholder="Answer:"
      v-model="new_answer"
    ></textarea>
    <div class="button-band">
      <button class="button is-link save-button" @click="click_cancel_new()">
        Cancel
      </button>
      <button
        class="button is-link save-button"
        v-if="!editing"
        @click="click_save_new(true)"
      >
        Save/Close
      </button>
      <button
        class="button is-link save-button"
        v-if="!editing"
        @click="click_save_new(false)"
      >
        Save/Continue
      </button>
      <button
        class="button is-link save-button"
        v-if="editing"
        @click="click_save_new(true)"
      >
        Save
      </button>
    </div>
  </article>
</template>

<script>
export default {
  name: "Input",
  data() {
    return {
      visible: false,
      editing: false,
      new_question: "",
      new_answer: "",
      new_question_class: "",
      new_answer_class: "",
    };
  },
  components: {},
  methods: {
    click_cancel_new() {
      this.new_question = "";
      this.new_answer = "";
      this.visible = false;
      this.$emit("submitted");
    },
    click_save_new(close) {
      if (this.new_question.trim().length === 0) {
        this.new_question_class = "is-danger";
        return;
      }
      if (this.new_answer.trim().length === 0) {
        this.new_answer_class = "is-danger";
        return;
      }
      this.$emit("submitted", [
        this.new_question.trim(),
        this.new_answer.trim(),
      ]);
      this.visible = !close;
      this.new_question = "";
      this.new_answer = "";
      this.new_question_class = "";
      this.new_answer_class = "";
    },
    open(item) {
      this.visible = true;
      if (item) {
        this.new_question = item.question;
        this.new_answer = item.answer;
        this.editing = true;
      } else {
        this.editing = false;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.button.is-link {
  min-width: 80px;
  margin-left: 20px;
}
textarea {
  margin-bottom: 20px;
}
.button-band {
  text-align: right;
}
.new-panel {
  padding: 20px;
}
</style>
