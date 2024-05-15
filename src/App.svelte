<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";

  import AddPoll from "./components/AddPoll.svelte";
  import Polls from "./components/Polls.svelte";

  import Tabs from "./shared/Tabs.svelte";

  // Changing active page
  let pages = [
    { title: "View Polls", id: 0 },
    { title: "Add Poll", id: 1 },
  ];

  let currentPage = 0;

  if (localStorage.getItem("currentPage")) {
    currentPage = parseInt(JSON.parse(localStorage.getItem("currentPage")));
  } else {
    currentPage = 0;
  }

  const changePage = (e, isExact) => {
    if (isExact) {
      currentPage = e;
    } else {
      currentPage = e.detail.id;
    }

    localStorage.setItem("currentPage", currentPage);
  };

  // Handling polls (showing, storing, getting from storage)
  let polls = [];

  if (!localStorage.getItem("polls")) {
    localStorage.setItem("polls", JSON.stringify(polls));
  } else {
    polls = JSON.parse(localStorage.getItem("polls"));
  }

  const addNewPoll = (e) => {
    changePage(0, true);

    const details = e.detail;

    const newPoll = {
      question: details.question,
      answerA: details.answerA,
      answerB: details.answerB,
      votesA: 0,
      votesB: 0,
      id: Math.random(),
    };

    polls = [newPoll, ...polls];

    localStorage.setItem("polls", JSON.stringify(polls));
  };

  const updatePolls = (e) => {
    const { option, id } = e.detail;

    let pollsCopy = [...polls];

    let pollToUpdate = pollsCopy.find((poll) => {
      return poll.id === id;
    });

    pollToUpdate[`votes${option.toUpperCase()}`] = ++pollToUpdate[`votes${option.toUpperCase()}`];

    polls = [...pollsCopy];

    localStorage.setItem("polls", JSON.stringify(polls));
  };
</script>

<Header></Header>
<Tabs {pages} {currentPage} on:clicked={(e) => changePage(e, false)}></Tabs>

{#if currentPage == 0}
  <Polls {polls} on:vote={(e) => updatePolls(e)}></Polls>
{:else if currentPage == 1}
  <AddPoll on:validForm={(e) => addNewPoll(e)}></AddPoll>
{:else}
  <div class="not-found">
    <h2>404 - PAGE NOT FOUND</h2>
  </div>
{/if}

<Footer></Footer>

<style>
  .not-found {
    display: flex;
    justify-content: center;
    padding: 1rem;
  }
</style>
