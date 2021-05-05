<template>
  <div class="container">
    <section class="hero is-navy">
      <div class="hero-head">
        <div class="top-bar"></div>
        <h1>Information</h1>
      </div>
    </section>
    <section>
      <article class="panel main-panel">
        <TopInfo v-if="false" />
        <div class="content">
          <div class="tabs">
            <ul>
              <li v-for="tab in tabs" :key="tab.id" :class="tab.cls">
                <a @click="click_tab(tab.id)">{{ tab.caption }}</a>
              </li>
            </ul>
          </div>
          <SelectQuestion v-if="tabs[0].cls == 'is-active'" ref="select" />
          <Answer v-if="tabs[1].cls == 'is-active'" ref="answer" />
        </div>
      </article>
      <Input @submitted="input_submit" ref="input" />
    </section>
    <footer class="footer">
      <article class="panel is-primary" v-if="tabs[1].cls == 'is-active'">
        <div class="tile is-parent is-10">
          <article class="tile is-child">
            <div class="panel-block">
              <button class="button is-link" @click="click_new()">New</button>
              <button class="button is-link" @click="click_edit()">Edit</button>
              <p class="control has-icons-left">
                <input
                  class="input"
                  type="text"
                  placeholder="Search"
                  v-model="search_key"
                  @blur="search_change"
                />
                <span class="icon is-left">
                  <i class="fas fa-search" aria-hidden="true"></i>
                </span>
              </p>
              <a class="clear-icon" @click="clear_search">
                <span> <i class="fas fa-times" aria-hidden="true"></i> </span
              ></a>
              <button class="button is-link" @click="click_save_file()">
                Save File
              </button>
            </div>
            <div class="panel-block import">
              <textarea class="import"
                placeholder="Imported Text:"
                v-model="import_text"
              ></textarea>
              <div class="button-band">
                <button
                  class="button is-link import-button"
                  @click="click_import()"
                >
                  Import
                </button>
              </div>
            </div>
          </article>
        </div>
      </article>
      <article class="panel is-primary">
        <div class="panel-block">
          <div class="tile is-ancestor">
            <div class="tile is-parent is-12">
              <article class="tile is-child footer-author">
                <p><strong>Vue 3 Programming With Bulma</strong> by Gary Sun</p>
              </article>
            </div>
          </div>
        </div>
      </article>
    </footer>
  </div>
</template>

<script>
import TopInfo from "../components/TopInfo.vue";
import SelectQuestion from "../components/SelectQuestion.vue";
import Answer from "../components/Answer.vue";
import Input from "../components/Input.vue";

export default {
  name: "Main",
  data() {
    return {
      tabs: [
        {
          caption: "Selection",
          id: 0,
          cls: "is-active",
        },
        {
          caption: "Answer Composation",
          id: 1,
          cls: "",
        },
        {
          caption: "Answer Selection",
          id: 2,
          cls: "",
        },
      ],
      new_question: "",
      new_answer: "",
      search_key: "",
      new_question_class: "",
      new_answer_class: "",
      import_text: "",
    };
  },
  components: { TopInfo, SelectQuestion, Answer, Input },
  methods: {
    click_tab(i) {
      this.tabs.forEach((tab) => (tab.cls = ""));
      this.tabs[i].cls = "is-active";
    },
    click_edit() {
      this.$refs["answer"].click_edit();
    },
    search_change() {
      this.$refs["answer"].search_changed(this.search_key);
    },
    click_save_file() {
      let export_file = this.$refs["answer"].click_save_file();
      window.open(export_file, "_blank");
    },
    input_submit(content) {
      this.$refs["answer"].click_save_new(content);
    },
    click_new() {
      this.$refs["answer"].click_edit(false);
      this.$refs.input.open();
    },
    clear_search() {
      this.search_key = null;
      this.search_change();
    },
    click_import() {
      this.$refs["answer"].import_text(this.import_text);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hero.is-navy {
  background-color: #4b6c9e;
  font-weight: 700;
  margin: 0px;
  padding: 0px 0px 0px 20px;
  color: #f9f9f9;
  border: none;
  line-height: 2em;
  font-size: 1.7em;
  text-align: left;
}
.main-panel {
  min-height: 800px;
  padding-bottom: 20px;
}
.container {
  text-align: left;
}
.footer {
  background-color: transparent;
  padding: 1.2em;
}
.content {
  margin: 30px;
}
.content ul {
  margin-left: 0;
}
.tile.is-child.box {
  background-color: transparent;
  box-shadow: none;
}
.footer-author {
  text-align: right;
}
.button.is-link {
  min-width: 80px;
  margin-left: 20px;
}
.panel:not(:last-child) {
  margin-bottom: 0;
}
footer .panel {
  box-shadow: none;
}
.control.has-icons-left {
  margin-left: 20px;
}
.icon.is-right {
  cursor: pointer;
}
.clear-icon {
  position: relative;
  left: -24px;
  color: #ccc;
}
.import {
  width: 890px;
  margin-left: 10px;
  justify-content:space-between
}
textarea.import{
  width:750px;
  height: 100px;
}
</style>
