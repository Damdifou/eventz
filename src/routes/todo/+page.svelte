<script>
    import {afterUpdate, onMount} from 'svelte';

    let todoItems = [];
    let newTodo = '';

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

    async function addTodo() {
        newTodo = newTodo.trim();
        if (!newTodo) return;

        const todo = {
            title: newTodo,
            completed: false
        };

        // Default options are marked with *
        await fetch(url, {
            method: "POST", // *GET, POST, PUT, DELETE, etc.
            body: JSON.stringify(todo), // body data type must match "Content-Type" header
        }).then(() => {
            fetch(url)
                .then(r => r.json())
                .then(data => {
                    todoItems = data;
                });
        });
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

                    <label class="cursor-pointer label">
                        <span class="label-text">{todo.title}</span>
                        <input type="checkbox" checked="checked" class="checkbox" value="{todo.completed}" on:click={() => toggleDone(todo.id)}>
                    </label>
                    <!--input id={todo.id} type="checkbox" value="{todo.completed}"/>
                    <label for={todo.id} class="tick " on:click={() => toggleDone(todo.id)}></label>
                    <span>{todo.title}</span-->
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
