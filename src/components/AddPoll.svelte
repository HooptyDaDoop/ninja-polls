<!--
  * TODO | Add question field
  * TODO | Create a single answer component (this is the correct answer)
  * TODO | Create 2 answer fields
  * TODO | Create a button to submit the form
  * TODO | When the form is submitted, check answer and question input fields for validation
  * TODO | If any fields are not long enough, create a component to let the user know. Don't submit form
  * TODO | Otherwise, emit a custom event to submit the form data
-->

<!-- MARK: Logic
-->
<script>
  import Button from "../shared/Button.svelte";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  let isValid = false;

  let poll = {
    question: "",
    answerA: "",
    answerB: "",
  };

  let errors = {
    question: "",
    answerA: "",
    answerB: "",
  };

  function validateForm() {
    isValid = true;

    if (poll.question.trim().length < 3) {
      errors.question = "Question must be at least 3 characters long.";
      isValid = false;
    } else {
      errors.question = "";
    }

    if (poll.answerA.trim().length < 1) {
      errors.answerA = 'Answer "A" can\'t be empty';
      isValid = false;
    } else {
      errors.answerA = "";
    }

    if (poll.answerB.trim().length < 1) {
      errors.answerB = 'Answer "B" can\'t be empty';
      isValid = false;
    } else {
      errors.answerB = "";
    }
  }

  function submitForm() {
    if (isValid == false) {
      console.log("Form is not valid");
      return;
    }

    poll.question = poll.question.charAt(0).toUpperCase() + poll.question.slice(1);

    poll.answerA = poll.answerA.charAt(0).toUpperCase() + poll.answerA.slice(1);

    poll.answerB = poll.answerB.charAt(0).toUpperCase() + poll.answerB.slice(1);

    dispatch("validForm", poll);

    poll.question = "";
    poll.answerA = "";
    poll.answerB = "";
  }
</script>

<!-- MARK: Content
-->
<div class="form-wrapper">
  <form on:submit|preventDefault={submitForm}>
    <div class="form-item question">
      <label for="question">Question</label>
      <input type="text" id="question" bind:value={poll.question} />
      <div class="error" class:error-pad={errors.question}>
        {errors.question}
      </div>
    </div>

    <div class="form-item answer">
      <label for="answer-a">Answer A</label>
      <input type="text" id="answer-a" bind:value={poll.answerA} />
      <div class="error" class:error-pad={errors.answerA}>{errors.answerA}</div>
    </div>

    <div class="form-item answer">
      <label for="answer-b">Answer B</label>
      <input type="text" id="answer-b" bind:value={poll.answerB} />
      <div class="error" class:error-pad={errors.answerB}>{errors.answerA}</div>
    </div>

    <div class="submit-btn">
      <Button buttonText="Send" isPrimary={true} on:onButtonClick={() => validateForm()}></Button>
    </div>
  </form>
</div>

<!-- MARK: Styles
-->
<style>
  .form-wrapper {
    display: flex;
    justify-content: center;
  }

  form {
    background-color: #f7f7f7;

    padding: 1rem;
    margin-bottom: 1rem;

    border-radius: 1rem;
  }

  .form-item {
    margin: 0.5rem;

    display: flex;
    flex-direction: column;
  }

  .form-item label {
    font-size: 1.25rem;
    font-weight: bold;
  }

  .form-item input {
    border-radius: 1rem;
    border: 1px solid black;
    padding: 0.5rem 1rem;
  }

  .error {
    color: crimson;
    background-color: #ffe8ed;

    border-radius: 0.5rem;
    margin: 0.25rem;

    user-select: none;
    transition: 150ms ease-in-out;
  }

  .error-pad {
    padding: 0.25rem 0.5rem;
  }
</style>
