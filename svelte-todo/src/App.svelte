<script>
    import { v4 as uuid } from "uuid";
    import Constant from "./constant";
    import TodoList from "./components/TodoList.svelte";
    import TodoHeader from "./components/TodoHeader.svelte";
    import TodoInfo from "./components/TodoInfo.svelte";

    let todoValue = "";

    let editMode = "";

    let viewMode = Constant.ALL;

    let todos = [
        {
            id: uuid(),
            content: "첫 번째 할일",
            done: false,
        },
        {
            id: uuid(),
            content: "두 번째 할일",
            done: false,
        },
        {
            id: uuid(),
            content: "세 번째 할일",
            done: true,
        },
        {
            id: uuid(),
            content: "네 번째 할일",
            done: false,
        },
    ];

    $: fetchTodos = todos;

    $: todoCount = fetchTodos.length;

    $: if (viewMode === Constant.ALL) {
        fetchTodos = todos;
    }

    $: if (viewMode === Constant.ACTIVE) {
        fetchTodos = todos.filter((todo) => todo.done === false);
    }

    $: if (viewMode === Constant.DONE) {
        fetchTodos = todos.filter((todo) => todo.done === true);
    }

    function handleCheckTodo(id) {
        todos = todos.map((todo) => {
            if (todo.id === id) {
                todo.done = !todo.done;
            }
            return todo;
        });
    }

    function handleTodoInputKeyup(event) {
        //console.log(event.keyCode);
        if (event.keyCode === 13) {
            addTodoItem();
        }
    }

    function addTodoItem() {
        if (todoValue) {
            const newTodo = {
                id: uuid(),
                content: todoValue,
                done: false,
            };
            todos = [...todos, newTodo];
            todoValue = "";
        }
    }

    function handleChangeEditMode(id) {
        editMode = id;
    }

    function handleEditTodoItem(editTodo) {
        todos = todos.map((todo) => {
            if (todo.id === editTodo.id) {
                todo = editTodo;
            }
            return todo;
        });
        editMode = "";
    }

    function handleRemoveTodo(id) {
        todos = todos.filter((todo) => todo.id !== id);
    }

    function handleChangeViewMode(mode) {
        viewMode = mode;
    }
</script>

<div class="app">
    <TodoHeader bind:todoValue {handleTodoInputKeyup} />
    <TodoInfo {todoCount} {handleChangeViewMode} {viewMode} />
    <TodoList {fetchTodos} {editMode} {handleChangeEditMode} {handleCheckTodo} {handleEditTodoItem} {handleRemoveTodo} />
</div>
