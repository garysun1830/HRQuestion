<template>
  <div>
    <AnswerItem
      v-for="q in questions"
      :key="q.id"
      :item="q"
      ref="item"
      @del_clicked="del_clicked"
      @submitted="input_submitted"
    />
  </div>
</template>

<script>
import AnswerItem from "../components/AnswerItem.vue";

export default {
  name: "Answer",
  components: { AnswerItem },
  data() {
    return {
      questions: [],
    };
  },
  created() {
    this.refresh();
  },
  methods: {
    save(items) {
      localStorage.setItem("questions", JSON.stringify(items));
    },
    refresh() {
      this.questions = JSON.parse(localStorage.getItem("questions"));
      if (this.questions) {
        this.questions.forEach((q) => (q.last_item = false));
        this.questions[this.questions.length - 1].last_item = true;
      }
    },
    click_save_new(item) {
      let new_id = this.questions[this.questions.length - 1].id + 1;
      let items = [
        ...this.questions,
        { question: item[0], answer: item[1], id: new_id, date: Date() },
      ];
      this.questions = items;
      this.save(this.questions);
      this.refresh();
    },
    click_edit() {
      this.$refs.item.forEach((it) => it.click_edit());
    },
    input_submitted(item) {
      this.questions.forEach((q) => {
        if (q.id == item.id) {
          q.question = item.question;
          q.answer = item.answer;
          q.date = Date();
        }
      });
      this.save(this.questions);
    },
    search_changed(search_key) {
      this.$refs.item.forEach((it) => it.search_changed(search_key));
    },
    del_clicked(id) {
      console.log(id);
      let items = [];
      this.questions.forEach((q) => {
        if (q.id !== id) {
          items.push(q);
        }
      });
      this.questions = items;
      this.save(this.questions);
    },
    click_save_file() {
      let dateFormat = require("dateformat");
      var file;
      var properties = { type: "text/plain" }; // Specify the file's mime-type.
      var data = [];
      this.questions.forEach((q) => {
        data.push(dateFormat(q.date, "dddd, mmmm dS, yyyy"));
        data.push("\n");
        data.push(q.question);
        data.push("\n");
        data.push(q.answer);
        data.push("\n\n");
      });
      try {
        // Specify the filename using the File constructor, but ...
        file = new File(data, "file.txt", properties);
      } catch (e) {
        // ... fall back to the Blob constructor if that isn't supported.
        file = new Blob(data, properties);
      }
      var url = URL.createObjectURL(file);
      console.log(url);
      return url;
    },
    import_text(text) {
      const strs = text.split("\n\n");
      const questions = [];
      let i = 1;
      strs.forEach((s) => {
        const q = {};
        const items = s.split("\n");
        if (items.length > 2) {
          q.id = i++;
          q.date = new Date();
          q.question = items[1];
          q.answer = items[2];
          questions.push(q);
        }
      });
      localStorage.setItem("questions", JSON.stringify(questions));
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
</style>