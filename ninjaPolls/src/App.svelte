<script>
	import Header from './components/Header.svelte'
	import Footer from './components/Footer.svelte'
	import Tabs from './shared/tabs.svelte'
	import PollList from './components/PollList.svelte'
	import CreatePollForms from './components/CreatePollForm.svelte'

	let items = ['Current Polls', 'Add neew Poll']
	let activeItem = 'Current Polls'

	const tagChange = (e) => {
		activeItem = e.detail
	}

	const handleAdd = e => {
		activeItem = 'Current Polls'
	}

</script>


<Header />
<main>
	<Tabs {items} {activeItem} on:tagChange={tagChange} />
	{#if activeItem === 'Current Polls'}
		<PollList />
	{:else if activeItem === 'Add neew Poll'}
		<CreatePollForms on:add={handleAdd} />
	{/if}
</main>
<Footer />

<style>
	main {
		max-width: 960px;
		margin: 40px auto
	}
</style>