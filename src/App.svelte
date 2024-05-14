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

	const changePage = (e) => {
		currentPage = e.detail.id;
	}
</script>

<Header></Header>
<Tabs {pages} {currentPage} on:clicked={changePage}></Tabs>

<Footer></Footer>

<style>
</style>