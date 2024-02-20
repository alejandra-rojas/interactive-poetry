
<script lang="ts">
	import { onMount } from "svelte";
	// import { wordList } from "./words";
  
	let wordList: string[] = ["sverdle", "poem", "about", "how", "more",];


	let randomWords: string[] = [];
	let poemWords: string[] = [];
	let regreted = false;

  
	console.log(poemWords)
	onMount(() => {
	  selectRandomWords();
	});
  
	function selectRandomWords() {
	  const randomIndexes: number[] = [];
	  while (randomIndexes.length < 3) {
		const randomIndex: number = Math.floor(Math.random() * wordList.length);
		if (!randomIndexes.includes(randomIndex)) {
		  randomIndexes.push(randomIndex);
		}
	  }
	  randomWords = randomIndexes.map((index) => wordList[index]);
	  console.log(wordList)
	}

	function addToPoem(word: any) {
		
	poemWords = [...poemWords, word];
	const updatedWordList = wordList.filter((w) => w !== word);
	wordList = updatedWordList
	console.log(poemWords);  

    }

	function regret(){
		if (!regreted && confirm("Do you want to regret and get new words?")) {
      selectRandomWords();
      regreted = true;
    }
    
	}


  </script>

<svelte:head>
	<title>Regret</title>
	<meta name="description" content="A Wordle clone written in SvelteKit" />
</svelte:head>

<h1 class="visually-hidden">Regret</h1>


	<a class="how-to-play" href="/sverdle/how-to-play">How to play</a>

	<div class="app-container">

		<div class="interaction-container">
			
			<div>
				<p>Select a word to start building your poem:</p>

			<div class="words-container">
				{#each randomWords as word}
					<button on:click={() => addToPoem(word)} class='word'>{word}</button>
				{/each}
			</div>

			</div>
			
			  
			
			{#if !regreted}
			  <button on:click={regret} class="word">Regrets ?</button>
			{/if}
		</div>

		<div class="selection-container">
			Your word selection
			{#each poemWords as word}<div class="word">{word}</div>{/each}
		</div>
			
	</div>
	







<style>

	.app-container {
		display: grid;
		grid-template-columns: 2fr 1fr;
	}
	
	.words-container{
		display: flex;
		justify-content: center;
		text-align: center;
		gap: 1rem;
	}

	.word {
		width: fit-content;
		display: flex;
		align-items: center;
		justify-content: center;
		text-align: center;
		box-sizing: border-box;
		text-transform: lowercase;
		border: none;
		font-size: calc(0.08 * var(--width));
		border-radius: 2px;
		background: white;
		padding: 0.5rem;
		color: rgba(0, 0, 0, 0.7);
	}

	.selection-container {
		display: flex;
		flex-direction: column;
		gap: .5rem;
	}

</style>
