<script>
	let todoItems = [];
	let newItem = "";
	function addItem(){
		newItem = newItem.trim();
		if(!newItem) return;
		let todo = {
			text: newItem,
			done: false,
			id: Date.now()
		};
		todoItems = [...todoItems, todo];
		newItem = "";
	}

	function toggleDone(id) {
		let index = todoItems.findIndex(item => item.id === Number(id));
		todoItems[index].done = !todoItems[index].done;
	}

	function deleteItem(id) {
		todoItems = todoItems.filter(item => item.id !== Number(id));
	}
</script>

<main>
	<div class="container">
		<h1>Todo's</h1>
		<ul>
			{#each todoItems as todo(todo.id)}
				<li class={todo.done? "done": ""}>
					<input on:click={() => toggleDone(todo.id)} id={todo.id} type="checkbox"/>
					<p>{todo.text}</p>
					<button on:click={() => deleteItem(todo.id)} class="delete-todo">
						<img src="images/delete.svg" alt="">
					</button>
				</li>
			{/each}
		</ul>
		<form on:submit|preventDefault={addItem}>
			<label for="todo"><img src="images/add.svg" alt=""></label>
			<input bind:value={newItem} type="text" id="todo">
		</form>
	</div>
</main>

<style>
	.container{
		background-color: #f4f4f4;
		width: 600px;
		margin-left: auto;
		margin-right: auto;
		padding: 20px;
		border-radius: 10px;
		flex-direction: column;
	}
	form, input{
		height: 35px;
	}
	form, li, .container {
		display: flex;
		justify-content: center;
		align-items: center;
	}
	input{
		margin: 0;
		padding: 0;
	}
	button {
		margin: 0;
		padding: 0;
		border: 0;
	}
	img, label, button{
		height: 25px;
		width: 25px;
	}
	label,p{
		margin: 5px;
	}
	ul{
		list-style: none;
		margin: 15px;
		padding: 0;
	}
	p{
		font-size: 18px;
	}

	.done{
		color: #cccccc;
	}
</style>