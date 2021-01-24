<svelte:options tag="async-component" />

<script>
	let userId = 0
	let name

	function setUserId (event) {
		name = '...'
		const id = event.target.userId.value
		fetch(`https://jsonplaceholder.typicode.com/users/${id}`)
			.then(response => response.json())
			.then(response => {
				name = response.name
			})
			.catch(() => {
				name = "Not found"
			})
	}
</script>

<div>
	<div>
		<strong>Current user: {name || ''}</strong>
	</div>
	<hr />
	<form on:submit|preventDefault={setUserId}>
		<input name="userId" type="text" defaultValue={userId} />
		<button type="submit">Submit</button>
	</form>
</div>
