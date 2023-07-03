<script>
    onMount(async () => {
        await fetch(`https://jsonplaceholder.typicode.com/todos/`)
            .then(r => r.json())
            .then(data => {
                continents = data;
            });
    })

    import {afterUpdate, onMount} from 'svelte';

    afterUpdate(() => {
        document.querySelector('.js-todo-input').focus();
    });

    let todoItems = [];
    let newTodo = '';

    function addTodo() {
        newTodo = newTodo.trim();
        if (!newTodo) return;

        const todo = {
            text: newTodo,
            checked: false,
            id: Date.now(),
        };

        todoItems = [...todoItems, todo];
        newTodo = '';
    }
    function toggleDone(id) {
        const index = todoItems.findIndex(item => item.id === Number(id));
        todoItems[index].checked = !todoItems[index].checked;
          }
    function deleteTodo(id) {
        todoItems = todoItems.filter(item => item.id !== Number(id));
    }
</script>
<main>
    <div class="container mx-auto px-center capitalize w-60">
        <blockquote class="text-2xl font-semibold italic text-center text-slate-900">
            <span class="before:block before:absolute before:-inset-1 before:-skew-y-3 before:bg-pink-500 relative inline-block">
    <span class="relative text-white">Todo</span>
  </span>

        </blockquote>
        <ul class="todo-list">
            {#each todoItems as todo (todo.id)}
                <li class="todo-item ">
                    <input id={todo.id} type="checkbox" />
                    <label for={todo.id} class="tick " on:click={() => toggleDone(todo.id)}></label>
                    <span>{todo.text}</span>
                    <button class="delete-btn btn-square bg-blue-500 rounded-lg flex-none w-20 h-10 " on:click={() => deleteTodo(todo.id)}>
                        <h1 class="app-title text-2xl">Delete</h1>
                        <svg><use href="#delete-icon"></use></svg>
                    </button>
                </li>
            {/each}
        </ul>
        <div class="empty-state">
            <svg class="checklist-icon"><use href="#checklist-icon"></use></svg>
            <h2 class="empty-state__title">Add your first todo</h2>
            <p class="empty-state__description">What do you want to get done today?</p>
        </div>
        <form on:submit|preventDefault={addTodo}>
            <input class="js-todo-input" type="text" aria-label="Enter a new todo item" placeholder="E.g. Build a web app" bind:value={newTodo}>
        </form>
    </div>
</main>