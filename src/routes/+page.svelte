
<script lang="ts">
	import { onMount } from "svelte";
	import { accordion } from './instructions'
	let isOpen = false;
	let showAppContainer = false;
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
  "annat", "än", "kött", "utredningen", "fick", "jag", "ångra", "du", "kommer", "alltid", "att", "bara", "förbli", "mitt", "nästan",
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

  
	function toggleAccordion() {
    isOpen = !isOpen;
  }

	function handleSubmit(){
		const newWords = userInput.split(/\s+/).filter(word => word.trim() !== "");
		wordList = [...wordList, ...newWords];
		userInput = "";
		selectRandomWords();
		showAppContainer = true; 
	}

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
	<title>Regrets</title>
	<meta name="description" content="A Wordle clone written in SvelteKit" />
</svelte:head>

<h1 class="visually-hidden">Regret</h1>


<div class="regrets-container">

	<div class="instructions">
		<a class="instructions-btn" on:click={toggleAccordion}> {#if isOpen}
			<svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
				<path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m15 9-6 6m0-6 6 6m6-3a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"/>
			  </svg>
		  {:else}
		  <svg class="w-6 h-6 text-gray-800 dark:text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
			<path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 11h2v5m-2 0h4m-2.6-8.5h0M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"/>
		  </svg>
		  {/if} Instruktioner </a>
	
		<div class="accordion" use:accordion={isOpen}>
		  <div class="instruction-text">
			<div><span class="bold">Välkommen att skapa en text ur ånger.</span> Skapandet sker i flera steg. 
			</div>
			<div><span class='orange'>Steg 1 har redan skett</span> 4 personer har skrivit text om ånger. Dessa texter har sedan rensats på skiljetecken och bildat en samling ord.
			</div>
			<div><span class='orange'>Steg 2</span> är att du skriver ord i rutan med rubriken Jag ångrar / jeg fortryder:. Dina ord läggs då till i den befintliga samlingen.
			</div>
			<div><span class='orange'>Steg 3</span> är att du väljer ord som i slutet bildar en ordföljd. Orden genereras slumpmässigt från samlingen ord, som du har varit med och skapat. Du börjar med att välja 1 av de 7 ord du får upp som första val. Varje valt ord generar i sin tur slumpmässigt 7 nya ord, unika till det ord du valt, som du sedan ska välja 1 av och fortsätter sedan på samma sätt. Du ställs totalt inför 13 val av ord att plocka, som i slutändan bildar en ordföljd på 13 ord. Under skapandets gång har du rätt att ångra dig max 3 gånger, och då gå tillbaka till tidigare steg för chansen att välja mellan andra ord som då genereras. 
			</div>
			<div><span class='orange'>Steg 4</span> är att du skapar en text utifrån den ordföljd du hamnat med. Det enda du kan ändra i ordföljden är att (1) lägga till versaler, (2) lägga till skiljetecken, (3) lägga till radbrytning.
			</div>
			<div><span class='orange'>Steg 5</span> är att du kan välja att kopiera den skapade texten och spara den hos dig, eller lämna sidan och låta den försvinna. När du lämnar sidan försvinner även de eventuella ord du la till i samlingen.
			</div>
		  </div>
		</div>
	</div>


	{#if !showAppContainer}
		<div class="step-one">
			<label for="inputField">Jag ångrar/ jeg fortryder:</label>
  			<textarea class="text-area" rows="6" id="inputField" bind:value={userInput} />
			
 			<button on:click={handleSubmit}>start</button>
		</div>
	{/if}
 

	{#if showAppContainer}
	<div class="app-container">
		{#if poemWords.length < 13}
			<div class="regret-container">	
				<div class="words-container">
				
					{#each randomWords as word}
						<button on:click={() => addToPoem(word)} class='word'>{word}</button>
					{/each}

				</div>
				{#if remainingRegrets > 0 && poemWords.length >= 1}
				  <button on:click={regret} class="regret-btn">Regrets?</button>
				{/if}
			</div>
		
				
				{#if poemWords.length >= 1}
				<div class="selection-list">
					{#each poemWords as word}
					<div class="selected-word">{word}</div>
					{/each}
				</div>	
				{/if}	
		{/if}

	</div>	

	<div class="step-three">
		{#if poemWords.length === 13}
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
		{/if}

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

		

	{/if}
</div>
	



	

	






<style>

	.regrets-container{
		height: 100%;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-items: center;
		flex: 1;
		gap: 1rem;
	}

	.instructions{
		display: flex;
        flex-direction: column;
        align-items: center;
        justify-items: center;
        width: 100%;
		max-width: 750px;
	}

	.instructions-btn{
		display: flex;
		align-items: center;
	}

	.instructions-btn svg{
		height: 25px;
	}

	.accordion {
		margin: 0.25rem 2rem;
		width: 100%;
		height: fit-content;
		background-color: rgba(255,255,255,0.5) ;
	}

	.instruction-text{
		font-size: 0.9rem;
		line-height: 120%;
		padding: 1rem 1.5rem 1.5rem;
		display: flex;
		flex-direction: column;
		gap: 0.75rem;
	}

	.bold{
		font-weight: 600;
		font-size: 1rem;
	}

	.orange{
		color: orangered;
	}

	.step-one{
		width: 100%;
		display: flex;
		flex-direction: column;
		gap: 1rem;
		align-items: center;
		font-size: 1.5rem;
	}

	.text-area {
		border: none;
		width: 90%;
		max-width: 600px;
		padding: 1rem;
		font-size: 1.5rem;
	}

	.step-one button{
		border: 0.5px solid gainsboro;
		padding:  0.5rem 1rem;
		color: gray;
	}

	.step-one button:hover{
		border: 0.5px solid black;
		color: black;
	}

	

	.app-container {
		width: 100%;
		display: grid;
		grid-template-columns: 4fr 1fr;
		gap: 2rem;		
	}

	.regret-container{
		display: flex;
		flex-direction: column;
	margin-top: 4rem;	}

	.words-container{		
		padding: 2rem 0.5rem;
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		text-align: center;
		gap: 0.5rem 1rem;
	}

	.regret-btn { 
		width: fit-content;
		display: flex;
		align-items: center;
		justify-content: center;
		text-align: center;
		box-sizing: border-box;
		text-transform: lowercase;
		border-radius: 2px;
		background: #EFEFEF;
		margin: 0 auto;
		border: 0.5px solid gainsboro;
		padding:  0.5rem 1rem;
		color: rgba(0, 0, 0, 0.5);;
	}

	.regret-btn:hover{
        border: 0.5px solid red;
        color: red;
    }

	.selection-list{
		margin: 5% 0;
		display: flex;
		flex-direction: column;
		gap: 0.1rem;
	}

	.word, .selected-word {
		width: fit-content;
		display: flex;
		align-items: center;
		justify-content: center;
		text-align: center;
		box-sizing: border-box;
		text-transform: lowercase;
		border: none;
		border-radius: 2px;
		background: white;
		padding: 0.5rem;
		color: rgba(0, 0, 0, 0.85);
	}

	.selected-word, .word:hover{
		color: black;
	}


	

 .selection-container{
	background-color: white;
	padding: 3rem 4rem;
	min-width: 200px;
 }

	.selection{
		cursor: pointer;
		width: fit-content;
		display: inline;
		text-align: center;
		box-sizing: border-box;
		border: none;
		/* font-size: calc(0.08 * var(--width)); */
		border-radius: 2px;
		color: rgba(0, 0, 0, 0.7);
		z-index: 100;
		line-height:225%;
	}

	.selected {
	padding: 0.25rem;
    outline: 0.5px solid orangered;
	z-index: 100;
}


	
   .formatting-options{
	display: flex;
		align-items: center;
		justify-content: center;
		box-sizing: border-box;
	margin-top: 2rem;
	gap: 0.2rem;
	}

	.formatting-options button {
		font-size: 0.8rem;
		width: fit-content;
		display: flex;
		align-items: center;
		justify-content: center;
		text-align: center;
		box-sizing: border-box;
		text-transform: uppercase;
		border-radius: 2px;
		/* background: #EFEFEF; */
		border: 0.5px solid gainsboro;
		padding:  0.5rem 1rem;
		color: rgba(0, 0, 0, 0.9);;
	}

	.formatting-options button:hover{
		border-color: black;
	}

</style>
