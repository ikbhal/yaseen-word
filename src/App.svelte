<script>
import {YaseenSurah} from './YaseenSurah';
// console.log("Yaseen Surah: ", YaseenSurah);
$:fullYaseen = YaseenSurah.join("\n");
let showSurahList = false;
let wordInterval= 1000;
let surahIndex = 0;
let surahWord = "";
function toggleSurahList() {
	showSurahList = !showSurahList;
}

function showSurahWord() {
	console.log("show surah word");
	if(surahIndex < YaseenSurah.length){
		surahWord = YaseenSurah[surahIndex];
		surahIndex ++;
	}else{
		surahWord = "End of Surah";
		// clear timer
		clearInterval(timer);
		timer = null;
	}
}
let timer = null;

function startSurahWordReading() {
	timer = setInterval(showSurahWord, wordInterval);
}

function stopSurahWordReading() {
	clearInterval(timer);
	timer = null;
}

</script>

<main>
	<h1>Yaseen Word by Word Reading</h1>
	<p>Show one Word from Yaseen . speed reading, show surah number</p>
	
	<!-- <p>Full Yaseen: {fullYaseen}</p> -->

	<div class="surahWordByWord">
		<h3>Surah Word By Word</h3>
		<button class="btn" on:click={startSurahWordReading}>Start Surah Word by Word Reading</button><br/>
		<button class="btn" on:click={stopSurahWordReading}>Stop Surah Word Reading</button><br/>
		<div class="word">{surahWord||"Not Started"}</div>
	</div>

	<button on:click={toggleSurahList}>Toglge Surah List</button>
	{#if showSurahList}
	<ol>
		{#each YaseenSurah as aayat, index}
		<li>{aayat}</li>
		{/each}
	</ol>
	{/if}
</main>

<style>
.surahWordByWord {
	width: 300px;
	height: 300px;
	border: 1px solid orange;
	padding: 30px;
}
.surahWordByWord h3{
	text-align: center;
	font-weight: bold;
}
.surahWordByWord .btn {
	width: 100%;
}
.surahWordByWord .word {
	margin-top: 20px;
	padding: 20px;
	text-align: center;
	background-color: black;
	color: white;
}
</style>