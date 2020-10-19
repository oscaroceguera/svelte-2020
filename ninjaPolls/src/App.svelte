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

	let polls = [
		{
			id: 1,
			question: 'python or js',
			answerA: 'python',
			answerB: 'js',
			votesA: 9,
			votesB: 15,
		}
	]

	const handleAdd = e => {
		const poll = e.detail;
		polls = [poll, ...polls]
		
	}

	const handleVote = (e) => {
		const {id, option } = e.detail;
		let copiedPolls = [...polls]
		let upvotedPoll = copiedPolls.find((poll) => poll.id == id)

		if (option === 'a') {
			upvotedPoll.votesA++
		}
		if (option === 'b') {
			upvotedPoll.votesB++
		}

		polls = copiedPolls
	}
</script>

<Header />
<main>
	<Tabs {items} {activeItem} on:tagChange={tagChange} />
	{#if activeItem === 'Current Polls'}
		<PollList {polls} on:vote={handleVote} />
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