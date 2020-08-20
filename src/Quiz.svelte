<script>
  import Header from "./Header.svelte";
  import Question from "./Question.svelte";
  import Loading from "./Loading.svelte";

  let corrAnswers = 0;
  export let category = 0;
  let Quiz = [];
  let currQuesNo = 1;

  const shuffle = (array) => {
    array.sort(() => Math.random() - 0.5);
  };
  const computeUrl = (category) =>
    `https://opentdb.com/api.php?amount=10&category=${category}`;

  const fetchQuiz = (url) => {
    fetch(url)
      .then((res) => res.json())
      .then((data) => {
        data.results.forEach((d) => {
          d.options = [...d.incorrect_answers, d.correct_answer];
          shuffle(d.options);
          d.selectedOption = null;
        });
        Quiz = data.results;
      })
      .catch((e) => console.log(e));
  };

  fetchQuiz(computeUrl(category));
</script>

<Header Qno={currQuesNo} on:exit {corrAnswers} />
{#each Quiz as Q, i}
  {#if currQuesNo === i + 1}
    <Question
      Ques={Q}
      Qno={currQuesNo}
      on:incrCorr={() => corrAnswers++}
      on:gotoNextQues={() => currQuesNo++}
      on:gotoPrevQues={() => currQuesNo--} />
  {/if}
{:else}
  <Loading />
{/each}
