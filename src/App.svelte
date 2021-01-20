<script>
	import Header from './components/Header.svelte'
	import Footer from './components/Footer.svelte'
	import PollList from './components/PollList.svelte'
	import PollForm from './components/PollForm.svelte'
    import Tabs from './shared/Tabs.svelte'
  let items = ['Current items', 'Add new item']
  let activeItem = 'Current items';
  let polls = [
  
  ]

  const tabChange = (e) =>{
   activeItem = e.detail;
  }

  const handleAdd = (e) =>{
   activeItem = 'Current items'
  }

 

</script>
<Header />
<main>
      <Tabs {items} {activeItem} on:tabChange={tabChange} />
      {#if activeItem === 'Current items'}
      <PollList  />
      {:else if activeItem === 'Add new item' }
     <PollForm on:add={handleAdd}/>

      {/if}

 
</main>
<Footer />
<style>
  :global(body){
    background: #f1f1f1;
  }
	main{
        max-width: 960px;
        margin: 40px auto;
        
    }
</style>