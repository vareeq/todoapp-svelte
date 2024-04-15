<script>
    // @ts-nocheck

    let todoList = [];
    let newItem = "";

    function removeFromList(index) {
        todoList = todoList.filter((item, i) => i !== index);
    }

    function addToList() {
        todoList = [...todoList, { text: newItem, status: false }];
        newItem = "";
    }

    function checkList(index) {
        todoList = todoList.map((item, i) =>
            i !== index ? item : { ...item, status: !item.status },
        );
    }
</script>

<h2>Todo List</h2>
<form>
    <input
        type="text"
        bind:value={newItem}
        size="30"
        placeholder="Add Todo List"
    /><button type="submit" on:click={addToList}>Add</button>
</form>

<div>
    <ol>
        {#each todoList as item, index}
            <li>
                <span class:checked={item.status}>{item.text}</span>
                {#if !item.status}
                    <span on:click={() => checkList(index)}>✔</span>
                {/if}
                <span on:click={() => removeFromList(index)}>❌</span>
            </li>
        {/each}
    </ol>
</div>

<style>
    .checked {
        text-decoration: line-through;
    }
</style>
