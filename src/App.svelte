<script>
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';

	import AddPoll from './components/AddPoll.svelte';
	import Polls from './components/Polls.svelte';

	import Tabs from './shared/Tabs.svelte';

	let pages = [
    {title: 'View Polls', id: 0},
    {title: 'Add Poll', id: 1},
  ];

  let currentPage = 0;

	if (localStorage.getItem('currentPage')) {
		currentPage = parseInt(
			JSON.parse(localStorage.getItem('currentPage'))
		)
	} else {
		currentPage = 0;
	}

	const changePage = (e) => {
		currentPage = e.detail.id;

		localStorage.setItem('currentPage', currentPage)
	}
</script>

<Header></Header>
<Tabs {pages} {currentPage} on:clicked={changePage}></Tabs>

{#if currentPage == 0}
	<Polls></Polls>
{:else if currentPage == 1}
	<AddPoll on:validForm={(e) => console.log(e.detail)}></AddPoll>
{:else}
	<h2>404 - PAGE NOT FOUND</h2>
{/if}

<Footer></Footer>

<style>
</style>