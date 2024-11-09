<script>
  import { createEventDispatcher } from "svelte";
  import Button from "../Sheard/button.svelte";
  import { v4 as uuidv4 } from "uuid";

  const dispatch = createEventDispatcher()

  let feilds = { question: "", answerA: "", answerB: "" };
  let errors = { question: "", answerA: "", answerB: "" };
  let valid = false;

  const submitHandler = () => {
    valid = true;
    //validate question
    if (feilds.question.trim().length < 5) {
      errors.question = "Question must be greater then 5 words";
      valid = false;
    } else {
      errors.question = "";
    }

    //validate answer A
    if (feilds.answerA.trim().length < 1) {
      errors.answerA = "Please check the answer A";
      valid = false;
    } else {
      errors.answerA = "";
    }

    //validate answer B
    if (feilds.answerB.trim().length < 1) {
      errors.answerB = "Please check the answer B";
      valid = false;
    } else {
      errors.answerB = "";
    }

    //create the new Poll
    if (valid) {
      const poll = {...feilds, 'votesA':0, 'votesB':0 , id:uuidv4()}
      dispatch('add',poll)
    }
  };
</script>

<form on:submit|preventDefault={submitHandler}>
  <div class="container animate-form">
    <div class="row pt-4">
      <div class="col-lg-6 col-sm-12 p-5 rounded-4">
        <div class="mb-3">
          <label for="formGroupExampleInput" class="form-label fw-bold"
            >Poll Question:</label
          >
          <input
            type="text"
            name="question"
            class="form-control border-black shadow"
            id="formGroupExampleInput"
            placeholder="Enter the Poll Question"
            bind:value={feilds.question}
          />
          <span class="error">{errors.question}</span>
        </div>
        <div class="mb-3">
          <label for="formGroupExampleInput" class="form-label fw-bold"
            >Answer A:</label
          >
          <input
            type="text"
            name="answer-a"
            class="form-control border-black shadow"
            id="formGroupExampleInput"
            placeholder="Answer A"
            bind:value={feilds.answerA}
          />
          <span class="error">{errors.answerA}</span>
        </div>
        <div class="mb-3">
          <label for="formGroupExampleInput" class="form-label fw-bold"
            >Answer B:</label
          >
          <input
            type="text"
            name="answer-b"
            class="form-control border-black shadow"
            id="formGroupExampleInput"
            placeholder="Answer B"
            bind:value={feilds.answerB}
          />
          <span class="error">{errors.answerB}</span>
        </div>
        <div class="pt-3 d-flex justify-content-around">
          <div>
            <Button flat={true}>Add Poll</Button>
          </div>
        </div>
      </div>
      <div class="col-lg-6 col-sm-12 p-5 rounded-4">
        <img src="/img/form.svg" class="fluid" alt="">
      </div>
    </div>
  </div>
</form>

<style>
  .error {
    color: red;
    font-size: 12px;
    font-weight: bold;
  }


  .animate-form {
      opacity: 0;
      transform: translateY(30px);
      animation: fadeInSlideUp 0.8s ease-in-out forwards;
    }

    @keyframes fadeInSlideUp {
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

</style>
