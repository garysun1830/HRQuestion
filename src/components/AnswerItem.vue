<template>
  <div>
    <div v-if="!changing">
      <label :class="question_hi_color">{{ item.question }} </label>
      <div class="answer">
        <label :class="answer_hi_color"> {{ item.answer }}</label>
      </div>
      <div class="edit-band" v-if="editing">
        <button class="button is-link" @click="click_edit_item()">Edit</button>
        <button class="button is-link" @click="click_del_item()">Delete</button>
      </div>
      <div>{{ format_date(item.date) }}</div>
    </div>
    <Input @submitted="input_submitted" ref="input" />
    <hr v-if="!item.last_item" />
  </div>
</template>

<script>
import Input from "../components/Input.vue";

export default {
  name: "AnswerItem",
  props: ["item"],
  components: { Input },
  data() {
    return {
      editing: false,
      question_hi_color: "",
      answer_hi_color: "",
      changing: false,
      dateFormat: require("dateformat"),
    };
  },
  methods: {
    click_edit(edit) {
      if (edit) {
        this.editing = edit;
      } else {
        this.editing = !this.editing;
      }
    },
    click_edit_item() {
      this.$refs.input.open(this.item);
      this.changing = true;
    },
    click_del_item() {
      this.$buefy.dialog.confirm({
        message: "Do you want to delete this item?",
        onConfirm: () => this.$emit("del_clicked", this.item.id),
      });
    },
    search_changed(search_key) {
      let empty = !search_key;
      if (!empty) {
        search_key = search_key.toLowerCase().trim();
        empty = !search_key;
      }
      if (empty) {
        this.question_hi_color = "";
        this.answer_hi_color = "";
        return;
      }
      if (this.item.question.toLowerCase().indexOf(search_key) == -1) {
        this.question_hi_color = "";
      } else {
        this.question_hi_color = "hi-color";
      }
      if (this.item.answer.toLowerCase().indexOf(search_key) == -1) {
        this.answer_hi_color = "";
      } else {
        this.answer_hi_color = "hi-color";
      }
    },
    input_submitted(item) {
      this.changing = false;
      if (item) {
        this.item.question = item[0];
        this.item.answer = item[1];
        this.$emit("submitted", this.item);
      }
    },
    format_date(d) {
      return this.dateFormat(d, "dddd, mmmm dS, yyyy");
    },
  },
};
</script>

<style scoped>
.answer {
  margin: 20px;
}
.answer label {
  font-weight: bold;
}
.edit-band {
  text-align: right;
}
label.hi-color {
  color: blue;
}
.button.is-link {
  min-width: 80px;
  margin-left: 20px;
}
</style>