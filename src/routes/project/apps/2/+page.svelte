<script>
    let newItem = '';
    let newItemAmount = '';
    let listOfExpenses = [];
    function addExpense() {
        if (newItem !== '') {
            listOfExpenses = [
                ...listOfExpenses,
                {
                    title: newItem,
                    amount: newItemAmount,
                },
            ];
            newItem = '';
            newItemAmount = '';
        }
    }
    function deleteExpense(index) {
        listOfExpenses.splice(index, 1);
        listOfExpenses = listOfExpenses;
    }
</script>

<main>
    <h1>Учет расходов</h1>  
    <form on:submit|preventDefault={addExpense}>
        <input bind:value={newItem} placeholder="Название">
        <input bind:value={newItemAmount} placeholder="Сумма">
        <button class="add-expense" on:click={addExpense}><span>+</span></button>
    </form>
    <table class="expenses">
        <tr>
            <td>Название</td>
            <td>Сумма</td>
            <td>Действие</td>
        </tr>
        {#each listOfExpenses as item, index}
            {#if !isNaN(+item.amount)  }
            <tr class="expense">
                <td><span class="expense_title">{item.title}</span></td>
                <td><span class="expense_amount">{+item.amount}</span></td>
                <td><button class="delete-expense" on:click={() => deleteExpense(index)}>Удалить</button></td>
            </tr>
            {/if}
        {/each}
    </table>
</main>

<style>
    tr:first-child {
        background-color: rgb(201, 214, 255);
    }
    td {
        padding: 1%;
        border: 3px solid rgb(218, 227, 255);
    }
    main {
        display: flex;
        flex-direction: column;
        align-items: center;
        min-height: 100%;
        padding: 5vmin;
        box-sizing: border-box;
    }    
    .expenses {
        width: 100%;
        font-size: 1.2rem;
        border-collapse: collapse;
    }
    input {
        flex-grow: 1;
        border: none;
        border-bottom: 1px solid black;
        background: transparent;
        font-size: 1.2rem;
        margin: 0 0 3% 0;
        outline: none;
    }
    button.add-expense {
        border-radius: 100%;
        border: 2px solid rgb(201, 214, 255);
        background-color: rgb(218, 227, 255);
        font-size: 20px;
    }
    button.delete-expense {
        background-color: rgb(218, 227, 255);
        font-size: 18px;
        border-radius: 5px;
        border: 3px solid rgb(201, 214, 255);
    }
    h1 {
        text-align: center;
        font-size: 1.5rem;
        margin: 2em 0;
    }
</style>