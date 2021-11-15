<script>
	let newTodo = ''
	let showCompleted = true
	let todos = [{
		name: 'Faire la lessive',
		completed: false
	},
	{
		name: 'Manger le porc',
		completed: true
	}]
	$: filteredTodos = todos.filter(t => showCompleted === true ? true : t.completed === false)
	function addTodo(){
		//e.preventDefault()
		todos = [...todos, {
			name: newTodo,
			completed: false
		}]
		
// 		todos.push({
// 			name: newTodo,
// 			completed: false
// 		})
// 		todos = todos // Detecter qu il y a eu un changement dans le todos
		
		newTodo = ''
	} 
	function changeTodo(todo){
		todos = todos.map(t => {
			if (t === todo){
				return {...todo, completed: !t.completed}
			}
			return t
		})
	}
</script>

<h1>Ma todolist</h1>
<label for=""><input type="checkbox" bind:checked={showCompleted}>Afficher les taches complétées</label>
<ul>
	{#each filteredTodos as todo}
	<li>
		<input type="checkbox" checked={todo.completed} on:change={() => changeTodo(todo)}>
		{todo.name}
	</li>
	{/each}
</ul>
<input type="text" bind:value={newTodo}> 
<!-- bind: permet d'eviter les onChange -->
<button on:click|preventDefault={addTodo}>Ajouter</button> 
<!-- preventDefault est equivalent au preventDefault qu'on devait mettre dans la fonction -->