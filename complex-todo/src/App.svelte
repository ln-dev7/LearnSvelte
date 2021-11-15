<script>
	import Todo from './Todo.svelte'
	let newTodo = ''
	let showCompleted = true
	let todos = []
	// {
	// 	name: 'Faire la lessive',
	// 	completed: false
	// },
	// {
	// 	name: 'Manger le porc',
	// 	completed: true
	// }
	$: filteredTodos = todos.filter(t => showCompleted === true ? true : t.completed === false)
	function addTodo(){
		if (newTodo != "") {
			todos = [...todos, {
				name: newTodo,
				completed: false
			}]	
		}
		else{
			alert("Veuillez entrer un champ")
		}
		
		newTodo = ''
	} 
	function changeTodo(todo, detail){
		todos = todos.map(t => {
			if (t === todo){
				return {...todo, ...detail}
			}
			return t
		})
	}
	function deleteTodo(todo){
		todos = todos.filter(t => t !== todo)
	}
</script>

<div class="container">
	<h1>Ma todolist</h1>
	<div class="new-todo">
		<input type="text" bind:value={newTodo}> 
		<button class="add" on:click|preventDefault={addTodo}>Ajouter</button> 
	</div>
	<ul>
		{#each filteredTodos as todo}
			<Todo 
			todo={todo} 
			on:delete={()=> deleteTodo(todo)}
			on:change={(e) => changeTodo(todo, e.detail)} 
			/>
		{/each}
	</ul>
	<label for=""><input type="checkbox" bind:checked={showCompleted}>Afficher les taches complétées</label>
</div>


<style>
	input{
        margin: 0.5rem;
    }
	.container{
		min-height: 50vh;
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
	}
    .add{
        background: #008cff;
		margin: 1rem;
        padding: 0.5rem;
        border-radius: 3px;
        overflow: hidden;
        color:white; 
        font-size:0.8rem;
		border: none;
        cursor: pointer;
    }
</style>