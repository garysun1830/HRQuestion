<template>
  <div>
    <div v-for="item in selections" :key="item.id">
      <label>{{ item.title }} </label>
      <div class="selection">
        <label class="radio-inline">
          <input type="radio" checked="checked" />{{ item.text }}</label
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SelectQuestion",
  data() {
    return {
      selections: [
        {
          title: `I certify that all information submitted is true and complete. I
      understand that any information provided by me through the hiring process
      that is found to be false or misrepresented in any respect, may eliminate
      me from further consideration.`,
          text: "Yes, I certify",
          id: 1,
        },
        {
          title: `Which of the following best describes your current status as an employee of the Province of British Columbia (BC Public Service)? Click the "i" for more information. `,
          text: "Regular full time or part time government employe",
          id: 2,
        },
        {
          title: `If you are a current or former BC Public Service employee, information concerning your past work performance may be collected from any public body within the BC Public Service for consideration in assessing your application for this opportunity.`,
          text: "Yes, I agree",
          id: 3,
        },
        {
          title: `To be considered for this opportunity you must be immediately eligible to accept permanent employment in Canada. Please confirm YOUR CURRENT CITIZENSHIP/IMMIGRATION STATUS ALLOWS YOU TO ACCEPT PERMANENT EMPLOYMENT IN CANADA. Click the "i" for more information `,
          text: "Yes",
          id: 4,
        },
        {
          title: `In the following section you will be required to provide complete, but concise responses in plain text format. Responses should be succinct (up to 200 words per response. Responses that exceed 250 words may not be captured in the system). Responses such as "see my resume" are unacceptable. Click the "i" for more information. `,
          text: "Yes, I understand",
          id: 5,
        },
        {
          title: `Please select the response that best describes your highest level of completed education in Computer Science or equivalent:`,
          text: "Master’s degree",
          id: 6,
        },
        {
          title: `Please select the response that best describes your experience in a lead developer role:`,
          text: "10 years or more",
          id: 7,
        },
      ],
    };
  },
};
</script>

<style scoped>
.selection {
  margin: 20px;
}
</style>