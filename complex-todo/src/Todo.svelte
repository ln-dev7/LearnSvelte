<script>
    import {createEventDispatcher} from 'svelte';
    import {fade} from 'svelte/transition';
    export let todo = {}
    const disptach = createEventDispatcher()
    function onCheck (){
        disptach('change', {completed: !todo.completed})
    }
    function onInput (e){
        disptach('change', {name: e.target.value})
    }
    function onDelete (){
        disptach('delete')
    }
</script>

<li transition:fade>
    <input type="checkbox" checked={todo.completed} on:change={onCheck}>
    <input type="text" value={todo.name} on:input={onInput}>
    <span class="delete" on:click|preventDefault={onDelete}>Supprimer</span>
</li>

<style>
    input{
        margin: 0.5rem;
    }
    .delete{
        background: red;
        padding: 0.5rem;
        border-radius: 3px;
        overflow: hidden;
        color:white; 
        font-size:0.8rem;
        cursor: pointer;
    }
    li{
		list-style-type: none;
	}
</style>