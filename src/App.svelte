<script>
  import CreatePollForm from "./components/CreatePollForm.svelte";
  import Footer from "./components/Footer.svelte";
  import Header from "./components/Header.svelte";
  import PollList from "./components/PollList.svelte";
  import Tabs from "./Sheard/Tabs.svelte";

  let items = ['Current Poll','Add New Poll'];
  let activeItem = 'Current Poll';

  const tabChange = (e) =>{
	activeItem =  e.detail
  }

    // polls
	let polls = [
    {
      id: 1,
      question: 'Python or JavaScript?',
      answerA: 'Python',
      answerB: 'JavaScript',
      votesA: 9,
      votesB: 15,
    },
  ];

// add new poll in array
  const handleAdd = (e) =>{
	polls = [...polls,e.detail];
	activeItem = 'Current Poll';
  }

  const handleVotes = (e)=>{
	const {option,id} = e.detail;
	let copiedPoll = [...polls]
	const result = copiedPoll.find((item)=> item.id == id);
	if(option === 'a'){
		result.votesA++;
	}
	if(option === 'b'){
		result.votesB++;
	}

	polls = copiedPoll

  }

</script>

<Header />
<div class="container">

<Tabs {items} {activeItem} on:tabChange={tabChange}/>
{#if activeItem === 'Current Poll'}
	<PollList {polls} on:vote={handleVotes}/>
{:else if  activeItem === 'Add New Poll'}
	 <CreatePollForm on:add={handleAdd}/>
{/if}

</div>
<Footer />

<style>
</style>
