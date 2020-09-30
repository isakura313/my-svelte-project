<script>
    let todos = [];
    let task = "";
    let filter = "all";

    function addTask(){
        todos = [{
            task:task,
            status: "urge",

        }, ...todos];
        task = "";
    }
    function markComplete(i){
        todos[i].status = "wait";
        todos = [...todos];
    }
    function removeTask(i){
        todos.splice(i, 1);
        todos = [...todos];
    }
</script>


<style>
.field_wrap{
    display: flex;
}
#icon_edit:hover{
    color: green;
    cursor: pointer;
}
#icon_delete:hover{
    color: red;
    cursor: pointer;
}
.task{
    display: grid;
    padding: 10px 5px;
    grid-template-columns: 80% 1fr 1fr;
    margin-bottom: 20px;
}

</style>


<div class="columns is-centered" style="margin-top: 30px">
    <div class="column is-one-quarter">
        <div class="field ">
        <div class="form field_wrap" >
            <input class="input" type="text" bind:value = {task}/>
            <button on:click={addTask}>
                Add
            </button>
        </div>
        </div>
        <div class="tasks">
            {#each todos as todo, i}

                    <div class="task">
                        <div>
                            {todo.task}
                        </div>
                        <span class="{todo.status='all'?'active':''} material-icons" on:click={()=>{markComplete(i)}} id="icon_edit">
                        done_outline
                        </span>
                        <span on:click={()=>{removeTask(i)}} class=" material-icons" id="icon_delete">
                         delete
                        </span>
                    </div>
                    {#if filter == "completed"}
                    {#if todo.status == 'completed'}
                        <div class="task">
                            <div>
                                {todo.task}
                            </div>
                            <span on:click={()=>{removeTask(i)}} class=" material-icons" id="icon_delete">
                                delete
                            </span>
                        </div>
                    {:else}
                        {#if todo.status == 'pending'}
                        <div class="task">
                            <div>{todo.task}</div>
                            <span on:click={()=>{removeTask(i)}} class=" material-icons" id="icon_delete">
                                delete
                            </span>
                        </div>
                        {/if}
                    {/if}
                    {/if}

                {/each}
              </div>
        <div class="filters">
            <button class="{filter='all'? 'active':'' }" on:click={()=>{filter='all'}}>
                All
            </button>
            <button class="{filter='completed'? 'active':'' }" on:click={()=>{filter='completed'}}>
                Complete
            </button>
            <button class="{filter='incomplete'? 'active':'' }" on:click={()=>{filter='incomplete'}}>
                Incomplete
            </button>

        </div>
    </div>
</div>
