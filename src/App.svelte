<script>
	import TextInput from "./UI/TextInput.svelte";
	import Radio from "./UI/Radio.svelte";

	let username = "";
	let words;
	let group;

	// Twitter search url
	$: Searchurl = defineUrl(words, username, group);

	document.onkeypress = function (event) {
		if (event.keyCode == 13) {
			console.log(Searchurl);
			window.open(Searchurl);
		}
	};

	function defineUrl(query, user, group) {
		if (group === "All of these words") {
			return (
				"https://twitter.com/search?q=(" +
				encodeURI(query) +
				")%20(from%3A" +
				user +
				")"
			);
		} else if (group === "Any of these words") {
			query = query.split(" ");
			let new_query = "";
			for (let i = 0; i < query.length - 1; i++) {
				new_query += query[i] + "%20OR%20";
			}
			new_query += query.pop();
			return (
				"https://twitter.com/search?q=(" +
				encodeURI(new_query) +
				")%20(from%3A" +
				user +
				")"
			);
		} else if (group === "This exact phrase") {
			return (
				'https://twitter.com/search?q=("' +
				encodeURI(query) +
				'")%20(from%3A' +
				user +
				")"
			);
		}
	}
</script>

<main>
	<h1>Advance Twitter Search</h1>
	<p class="description">Use this form to help you make more advanced twitter searches easily.</p>

	<TextInput bind:value={username} placeholder="elonmusk">Username</TextInput>
	<TextInput bind:value={words} placeholder={group}>Search for:</TextInput>
	<Radio
		bind:group
		options={[
			"All of these words",
			"This exact phrase",
			"Any of these words",
		]}
	/>

	<a class="button" href={Searchurl} target="_blank">Search</a>
</main>
<div class="signature">
	<p>
		Built with ❤️ by <a href="https://twitter.com/ferminrp">ferminrp</a>
	</p>
</div>

<style>
	main {
		width: 90%;
		max-width: 720px;
		margin-left: auto;
		margin-right: auto;
	}
	h1 {
		color: #1b91db;
	}

	.description {
		color: #888;
		margin-bottom: 2rem;;
	}

	.button {
		background-color: #1b91db;
		color: white;
		font-weight: bold;
		border-radius: 5px;
		padding: 0.5rem 2rem;
		margin-top: 2rem;
	}

	.signature {
		width: 100%;
		position: fixed;
		bottom: 2rem;
	}

	.signature p {
		text-align: center;
	}

</style>
