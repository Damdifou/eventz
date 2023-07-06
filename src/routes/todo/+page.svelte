<script>

    import {onMount} from 'svelte';
    import TodoList from './TodoList.svelte';
    const url = `https://todoback.nos.bzh/api/todos`;

    let todos = [];

    onMount(async () => {
        await fetch(url)
            .then(r => r.json())
            .then(data => {
                todos= data;
            });
    })
    async function addTodo(name) {
        await fetch(url, {
            method: "POST", // *GET, POST, PUT, DELETE, etc.
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                "id": null,
                "name": name,
                "content": "Indium",
                "done": false,
                "tags": null,
                "login": null
            } ), // body data type must match "Content-Type" header
        }).then(() => {
            fetch(url)
                .then(r => r.json())
                .then(data => {
                    todos = data;
                });
        });
    }

</script>

<div class="board">
    <input
            placeholder="what needs to be done?"
            on:keydown={(e) => {
			if (e.key === 'Enter') {
				addTodo(e.currentTarget.value);
				e.currentTarget.value = '';
			}
		}}
    />

    <div class="todo">
        <h2>todo</h2>
        <TodoList todos={todos} done={false} />
    </div>


</div>

<style>
    .board {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-column-gap: 1em;
        max-width: 36em;
        margin: 0 auto;
    }

    .board > input {
        font-size: 1.4em;
        grid-column: 1/3;
        padding: 0.5em;
        margin: 0 0 1rem 0;
    }

    h2 {
        font-size: 2em;
        font-weight: 200;
    }
</style>
