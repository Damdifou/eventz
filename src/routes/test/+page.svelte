<script>
    import {afterUpdate, onMount} from 'svelte';
    let todos = [
        { done: false, text: 'finish Svelte tutorial' },
        { done: false, text: 'build an app' },
        { done: false, text: 'world domination' }
    ];
    const url = `https://jsonplaceholder.typicode.com/todos/`;

    onMount(async () => {
        await fetch(url)
            .then(r => r.json())
            .then(data => {
                todoItems = data;
            });
    })
    afterUpdate(() => {
        document.querySelector('.js-todo-input').focus();
    });

    function add() {
        todos = todos.concat({
            done: false,
            text: ''
        });
    }

    function clear() {
        todos = todos.filter((t) => !t.done);
    }

    $: remaining = todos.filter((t) => !t.done).length;
</script>

<div class="centered">
    <h1>todos</h1>

    <ul class="todos">
        {#each todos as todoItem}
            <li class:done={todoItem.done}>
                <input
                        type="checkbox"
                        bind:checked={todoItem.done}
                />

                <input
                        type="text"
                        placeholder="What needs to be done?"
                        bind:value={todoItem.text}
                />
            </li>
        {/each}
    </ul>

    <p>{remaining} remaining</p>

    <button on:click={add}>
        Add new
    </button>

    <button on:click={clear}>
        Clear completed
    </button>
</div>


<style>
    .centered {
        max-width: 20em;
        margin: 0 auto;
    }

    .done {
        opacity: 0.4;
    }

    li {
        display: flex;
    }

    input[type="text"] {
        flex: 1;
        padding: 0.5em;
        margin: -0.2em 0;
        border: none;
    }
</style>