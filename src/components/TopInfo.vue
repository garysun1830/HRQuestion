<template>
  <div class="box">
    <h3>{{ title }}</h3>
    <div class="top-info">
      {{ body }}
    </div>
  </div>
</template>

<script>
export default {
  name: "TopInfo",
  data() {
    return {
      title: "Question/Answers I made for B.C. Public Services",
      body: `SYSTEM TIME OUT: You will be automatically logged out of the system after
      60 minutes. To ensure you do not lose any information you have entered, we
      recommend that you save often. To save your application, click ‘Finish
      Later’ at the bottom of the page. Your saved application will appear on My
      Resumes> Resume Submission History page in a section labeled ‘Incomplete
      Applications’. We recommend saving frequently while completing the
      questionnaire. You can also copy the questions into another document and
      paste the responses when you are ready.`,
    };
  },
};
</script>

<style scoped>
.box {
  border-radius: 0;
}
h3 {
  font-weight: bold;
}
.top-info {
  margin-top: 20px;
}
</style>