<script>
    import { flip } from 'svelte/animate';
    import { send, receive } from './transition.js';
    export let todos;

    const url = `https://todoback.nos.bzh/api/todos`;



    async function deleteTodo(id) {
        await fetch(url + "/" + id, {
            method: "DELETE", // *GET, POST, PUT, DELETE, etc.

        }).then(() => {
            fetch(url)
                .then(r => r.json())
                .then(data => {
                    todos = data;
                });
        });
    }

</script>

<ul class="todos">
    {#each todos as todo (todo.id)}
        <li
                in:receive={{ key: todo.id }}
                out:send={{ key: todo.id }}
                animate:flip={{ duration: 200 }}
        >
            <label>
                <input
                        type="checkbox"
                        bind:checked={todo.done}
                        on:change={(e) => todos.mark(todo, e.currentTarget.checked)}
                />

                <span>{todo.name}</span>

                <button class="btn btn-ghost rounded-btn" on:click={() => deleteTodo(todo.id)} aria-label="Remove" >
                    delete
                </button>

            </label>
        </li>
    {/each}
</ul>

<style>
    label {
        width: 100%;
        height: 100%;
        display: flex;
    }

    span {
        flex: 1;
    }

    button {
        background-image: url(./remove.svg);
    }
</style>