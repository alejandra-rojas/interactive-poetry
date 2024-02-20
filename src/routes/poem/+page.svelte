
<script lang="ts">
	import { onMount } from "svelte";
  
	let userInput = "";
	let wordList: string[] = [
  "jeg", "fortryder", "ikke", "hjertesorgen", "at", "jeg", "gik", "hjemmefra", "den", "nat",
  "jeg", "fortryder", "ikke", "at", "jeg", "greb", "ud", "efter", "nogen", "jeg", "fortryder",
  "ikke", "de", "fremmede", "ansigter", "deres", "kander", "og", "glas", "og", "deres", "beskyttende",
  "øjne", "og", "deres", "broderskab", "at", "jeg", "var", "som", "en", "søster", "jeg", "fortryder",
  "ikke", "at", "jeg", "hældte", "ud", "af", "mig", "selv", "jeg", "fortryder", "ikke", "at", "jeg",
  "lod", "mig", "bære", "jeg", "fortryder", "ikke", "at", "jeg", "lod", "mig", "køre", "med", "i",
  "deres", "bil", "at", "jeg", "ikke", "ønskede", "natten", "skulle", "stoppe", "at", "jeg", "ikke",
  "ville", "give", "slip", "på", "ansigterne", "og", "omsorgen", "i", "ordene", "uden", "for", "mig",
  "selv", "jeg", "fortryder", "ikke", "at", "jeg", "så", "et", "menneske", "og", "rakte", "ud", "efter",
  "det", "jeg", "fortryder", "ikke", "mit", "hjertes", "stædighed", "viljen", "efter", "at", "skabe",
  "skønhed", "i", "en", "grim", "nat", "viljen", "efter", "at", "grave", "barnet", "ud", "af", "manden",
  "der", "var", "som", "en", "dreng", "han", "lignede", "en", "dreng", "han", "lignede", "alle", "de",
  "mænd", "der", "fyldte", "mit", "hoved", "som", "en", "playliste", "på", "spotify", "jeg", "har", "glemt",
  "hans", "navn", "men", "det", "sidder", "på", "tungen", "jeg", "har", "glemt", "datoen", "men", "jeg",
  "mærker", "årstiden", "alle", "de", "dage", "han", "invaderede", "jeg", "har", "ikke", "glemt", "dem",
  "jeg", "har", "et", "lille", "alter", "kun", "for", "ham", "det", "folder", "sig", "sammen", "som", "en",
  "papkasse", "inde", "i", "papkassen", "er", "der", "små", "lufttætte", "poser", "noget", "af", "ham", "jeg",
  "ikke", "kan", "fortrydedet", "jag", "inte", "får", "ångra", "det", "jag", "inte", "kan", "ångra", "eftersom",
  "det", "inte", "var", "min", "handling", "och", "jag", "har", "inte", "rätt", "att", "ångra", "passivitet",
  "vänner", "säger", "det", "reportagen", "säger", "det", "vården", "rösterna", "jaget", "litteraturen", "det",
  "finns", "inte", "rum", "för", "min", "handling", "och", "då", "inget", "att", "ta", "tillbaka", "inget", "att",
  "göra", "om", "möjligtvis", "alkoholen", "men", "det", "är", "en", "problematisk", "anklagelse", "rum", "finns",
  "för", "att", "ångra", "alkohol", "men", "inte", "i", "det", "trapphuset", "inte", "i", "den", "fuskpälsen", "med",
  "de", "tuttarna", "min", "syster", "ångrar", "åt", "mig", "att", "jag", "inte", "grät", "på", "ett", "café", "i",
  "ett", "fönster", "att", "jag", "inte", "visade", "på", "vilket", "sätt", "det", "gjorde", "ont", "så", "att", "hon",
  "också", "kunde", "gråta", "i", "stället", "för", "att", "stirra", "blankt", "bort", "mot", "cykelstället", "andra",
  "ångrar", "åt", "mig", "att", "jag", "inte", "blev", "arg", "men", "när", "jag", "inte", "får", "bli", "arg", "på", "mig",
  "själv", "finns", "det", "ingen", "riktning", "han", "är", "konturlös", "ett", "suddigt", "sladdrigt", "minne", "oförmågan",
  "till", "sanning", "skaver", "men", "det", "är", "inte", "ånger", "andras", "kroppar", "finns", "det", "känns", "ibland",
  "att", "vara", "kopplad", "till", "andras", "smärta", "att", "svika", "dem", "eventuellt", "lögnerna", "kanske", "jag", "ångrar",
  "de", "enda", "sanna", "orden", "jag", "minns", "är", "att", "jag", "förstod", "att", "min", "kropp", "inte", "är", "något",
  "annat", "än", "kött", "utredningen", "fick", "jag", "ångradu", "kommer", "alltid", "att", "bara", "förbli", "mitt", "nästan",
  "och", "inte", "bara", "på", "ett", "världsligt", "plan", "där", "det", "ytliga", "och", "genomskådliga", "stiger", "fram", "för",
  "att", "beskriva", "ett", "förflutet", "för", "att", "sätta", "ord", "krävs", "tydningar", "på", "ett", "djupt", "spirituellt", "och",
  "introspektivt", "plan", "bortom", "allt", "vi", "drömde", "om", "att", "bli", "men", "aldrig", "riktigt", "blev", "återfinner", "jag",
  "fortfarande", "din", "skepnad", "som", "en", "bilaga", "i", "varje", "konversation", "skratt", "och", "ensamma", "stund", "jag", "har",
  "dyker", "upp", "likt", "en", "förlängd", "arm", "som", "alltid", "kommer", "vara", "den", "saknade", "pusselbiten", "i", "fullbordandet",
  "av", "varje", "rum", "jag", "är", "i", "vars", "brist", "alltid", "kommer", "lämna", "ett", "utrymme", "inkomplett", "du", "kommer", "alltid",
  "att", "vara", "den", "som", "hamnade", "i", "kläm", "mellan", "min", "oförmåga", "att", "välja", "vilken", "av", "hjärnhalvorna", "att", "sätta",
  "min", "tillit", "till", "är", "jag", "menad", "att", "vandra", "denna", "jord", "som", "en", "rationell", "strateg", "eller", "en", "intuitiv",
  "fritänkare", "vad", "styrs", "jag", "egentligen", "av", "hur", "fortsätter", "jag", "leva", "med", "det", "efteråt", "och", "jag", "kanske",
  "har", "gjort", "fel", "i", "att", "ha", "förlitat", "mig", "på", "en", "myt", "som", "säkert", "har", "blivit", "avslöjad", "som", "falsk", "av",
  "hela", "det", "medicinska", "samfundet", "därför", "kommer", "du", "också", "alltid", "att", "vara", "den", "som", "fått", "mig", "att", "omvärdera",
  "sättet", "jag", "klänger", "fast", "vid", "ett", "specifikt", "personlighetsdrag", "för", "något", "positivt", "måste", "ha", "växt", "utav", "att",
  "du", "aldrig", "blev", "mer", "än", "bara", "ett", "nästan", "du", "kunne", "have", "gjort", "det", "anderledes", "fortalt", "at", "du", "var", "syg",
  "fortalt", "at", "du", "måske", "ikke", "kom", "tilbage", "at", "næste", "gang", "vi", "mødtes", "var", "du", "en", "anden", "du", "kunne", "have",
  "inddraget", "mig", "i", "din", "tvivl", "i", "din", "angst", "bare", "et", "eller", "andet", "eller", "lægerne", "eller", "de", "andre", "voksne",
  "hvem", "kan", "jeg", "begræde", "i", "var", "så", "naive", "han", "var", "så", "naiv", "et", "privilegie", "at", "være", "barnet", "i", "fortællingen",
  "nej", "tolv", "år", "er", "ikke", "et", "barn", "nu", "kan", "du", "ikke", "fortryde", "kun", "forfølge", "lucky", "you", "easy", "way", "out", "is",
  "it", "a", "gift", "or", "a", "curse", "fortiden", "forgriber", "sig", "på", "dem", "som", "hun", "gør", "på", "mig", "vil", "gerne", "huske", "hende",
  "rigtigt", "undskyld", "men", "jeg", "var", "fuld", "mennesker", "er", "også", "bare", "mennesker", "all", "those", "excuses", "a", "counterfactual", "emotion",
  "at", "græde", "over", "spildt", "mælk", "what", "a", "coward", "fratager", "mig", "ansvaret", "gør", "hvad", "de", "regner", "med", "giver", "dem", "ret",
  "giver", "dig", "ret", "det", "er", "nok", "mest", "sorgen", "over", "at", "have", "gjort", "dig", "så", "ked", "af", "det", "samvittigheden", "men", "snart",
  "kan", "jeg", "bare", "ikke", "fortryde", "længere", "don't", "haunt", "me", "anymore", "it's", "not", "you", "it's", "me", "kan", "ikke", "love", "noget",
  "yes", "no", "maybe", "det", "er", "et", "privilegie", "at", "kunne", "fortryde", "tage", "beslutninger", "hvem", "hvor", "længe", "hvordan", "hvor", "mange",
  "hvorhenne", "say", "yes", "to", "the", "dress", "min", "mormor", "sagde", "I", "sommers", "I", "knew", "three", "days", "after", "I", "married", "him",
  "I", "had", "made", "the", "biggest", "mistake", "of", "my", "life", "nervous", "laugh"
];

	let randomWords: string[] = [];
	let sessionWordSet: string[][] = [];

	let poemWords: string[] = [];

	let remainingRegrets = 3;

  
	// onMount(() => {
	//   selectRandomWords();
	// });
  
	function handleSubmit(){
		const newWords = userInput.split(/\s+/).filter(word => word.trim() !== "");
		wordList = [...wordList, ...newWords];
		userInput = "";
		console.log(wordList)
		selectRandomWords();

	}

	console.log(wordList)

	function selectRandomWords() {
	  const randomIndexes: number[] = [];
	  while (randomIndexes.length < 7) {
		const randomIndex: number = Math.floor(Math.random() * wordList.length);
		if (!randomIndexes.includes(randomIndex)) {
		  randomIndexes.push(randomIndex);
		}
	  }
	  randomWords = randomIndexes.map((index) => wordList[index]);
	  sessionWordSet.push([...randomWords]);
	}
  
	function addToPoem(word: any) {
	  poemWords = [...poemWords, word];
	//   const updatedWordList = wordList.filter((filteredWord) => filteredWord !== word);
	//   wordList = updatedWordList;
	  selectRandomWords();
	  console.log(sessionWordSet)
	}
  
	function regret() {
	  if (remainingRegrets > 0 && confirm("Do you want to give one step back?")) {
		sessionWordSet.pop();
		poemWords.pop();
		poemWords = poemWords;
		randomWords = [...sessionWordSet[sessionWordSet.length - 1]];
		remainingRegrets -= 1;

	  }
	}

	let selectedWordIndex: number | null = null;

	let modifiedWords: string[] = [];

function selectWord(index: number) {
  selectedWordIndex = selectedWordIndex === index ? null : index;
}

function capitalizeWord(index: number) {
  if (!modifiedWords[index]) {
    modifiedWords[index] = poemWords[index];
  }
  poemWords[index] = poemWords[index].charAt(0).toUpperCase() + poemWords[index].slice(1);
}

function addComma(index: number) {
  if (!modifiedWords[index]) {
    modifiedWords[index] = poemWords[index];
  }
  poemWords[index] += ",";
}

function addSlash(index: number) {
  if (!modifiedWords[index]) {
    modifiedWords[index] = poemWords[index];
  }
  poemWords[index] += "/";
}

function addPoint(index: number) {
  if (!modifiedWords[index]) {
    modifiedWords[index] = poemWords[index];
  }
  poemWords[index] += ".";
}

function addLinebreak(index: number) {
  if (!modifiedWords[index]) {
    modifiedWords[index] = poemWords[index];
  }
  poemWords[index] += '<br>';
}

function restore(index: number) {
  if (modifiedWords[index]) {
    poemWords[index] = modifiedWords[index];
    modifiedWords[index] = "";
  }
}



	
  </script>

<svelte:head>
	<title>Regret</title>
	<meta name="description" content="A Wordle clone written in SvelteKit" />
</svelte:head>

<h1 class="visually-hidden">Regret</h1>


<label for="inputField">Jag ångrar/ jeg fortryder:</label>
  <input type="text" id="inputField" bind:value={userInput} />

  <button on:click={handleSubmit}>Submit</button>

    <!-- <input placeholder="Jag ångrar/ jeg fortryder" type='text' maxlength=200 /> -->

	<a class="how" href="/sverdle/how-to-play">Instruktioner</a>

	<div class="app-container">

		{#if poemWords.length < 13}
		<div class="interaction-container">
			
			<div>

			<div class="words-container">
			
				{#each randomWords as word}
					<button on:click={() => addToPoem(word)} class='word'>{word}</button>
				{/each}
			
			</div>

			</div>
			
			{#if remainingRegrets > 0}
			  <button on:click={regret} class="word regret">Regrets ?</button>
			{/if}
		</div>
		
		{/if}

		

	<div >


  <div class="selection-container">
	{#each poemWords as word, index}
    {#if selectedWordIndex === index}
      <div
        role="button"
        aria-pressed={selectedWordIndex === index}
        class="selection selected"
        on:click={() => selectWord(index)}
      >
	  {@html word}
      </div>
    {:else}
      <div
        role="button"
        aria-pressed={selectedWordIndex === index}
        class="selection"
        on:click={() => selectWord(index)}
      >
	  {@html word}
      </div>
    {/if}
  {/each}
  </div>
  <div>

	{#if selectedWordIndex !== null}
	<div class="formatting-options">
	  <button on:click={() => capitalizeWord(selectedWordIndex)}>C</button>
	  <button on:click={() => addComma(selectedWordIndex)}>,</button>
	  <button on:click={() => addSlash(selectedWordIndex)}>/</button>
	  <button on:click={() => addPoint(selectedWordIndex)}>.</button>
	  <button on:click={() => restore(selectedWordIndex)}>RESET</button>
      <button on:click={() => addLinebreak(selectedWordIndex)}>ENTER</button>
	  
	</div>
  {/if}
  </div>

		  </div>
			
	</div>
	







<style>

	.app-container {
		display: grid;
		grid-template-rows:  1fr 1fr;
	}

	.how{
		margin: 0 auto;
	}
	
	.words-container{
		padding-top: 30%;
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
		/* font-size: calc(0.08 * var(--width)); */
		border-radius: 2px;
		background: white;
		padding: 0.5rem;
		color: rgba(0, 0, 0, 0.7);
	}

	.regret { margin: 10% auto;}


 .selection-container{
	background-color: white;
	padding: 3rem 4rem;
 }

	.selection{
		width: fit-content;
		display: inline;
		text-align: center;
		box-sizing: border-box;
		border: none;
		/* font-size: calc(0.08 * var(--width)); */
		border-radius: 2px;
		color: rgba(0, 0, 0, 0.7);
		z-index: 100;
		line-height:250%;
	}

	.selected {
		padding: 0.5rem;
    outline: 2px solid orange;
	z-index: 100;}


	
   .formatting-options{
	display: flex;
		align-items: center;
		justify-content: center;
		box-sizing: border-box;
	margin-top: 3rem;
	gap: 0.2rem;
	}

	.formatting-options button {
		color: black ;
		width: fit-content;
		text-align: center;
		text-transform: uppercase;
		border: none;
		font-size: calc(0.08 * var(--width));
		border-radius: 2px;
		background: white;
		padding: 0.5rem;
	}

</style>
