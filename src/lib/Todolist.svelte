<script lang="ts">
  interface TodoItem {
    id: number
    text: string
    done: boolean
  }

  let todolist: TodoItem[] = JSON.parse(localStorage.getItem('todolist')) || []
  let todo = ''
  $: localStorage.setItem('todolist', JSON.stringify(todolist))

  const todoAdd = (e: KeyboardEvent) => {
    if (e.code === 'Enter') {
      const text = (e.target as HTMLInputElement).value.trim()
      if (text) {
        const id = todolist.length ? todolist[todolist.length - 1].id + 1 : 1
        const todoItem: TodoItem = {
          id,
          text,
          done: false
        }
        todolist = [...todolist, todoItem]
        todo = ''
      }
    }
  }

  const todoToggle = (item: TodoItem) => {
    todolist.forEach((todo) => {
      if (todo.id === item.id) todo.done = !todo.done
    })
    todolist = [...todolist]
  }

  const todoRemove = (item: TodoItem) => {
    todolist = todolist.filter((todo) => todo.id !== item.id)
  }
</script>

<h1>My Todos</h1>

<input bind:value={todo} on:keydown={todoAdd} placeholder="What needs to be done?" type="text" />

<ul class="todolist">
  {#each [...todolist].reverse() as todoItem (todoItem.id)}
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <li class={todoItem.done ? 'done' : ''} on:click={() => todoToggle(todoItem)}>
      <span>{todoItem.text}</span>
      <i on:click={() => todoRemove(todoItem)} title="Delete">+</i>
    </li>
  {/each}
</ul>

<style lang="less">
  input[type='text'] {
    font-size: 1em;
    font-weight: 500;
    font-family: inherit;
    min-width: 60vw;
    text-align: center;
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 0.6em 1.2em;
    transition: border-color 0.25s;

    &:hover {
      border-color: #646cff;
    }

    &:focus,
    &:focus-visible {
      outline: 2px auto #333;
    }
  }

  .todolist {
    text-align: left;
    padding: 0;

    & > li {
      border: 1px solid #ccc;
      border-radius: 4px;
      list-style: none;
      word-break: break-all;
      padding: 0.4em 2em 0.4em 0.4em;
      cursor: pointer;
      position: relative;
      transition: border-color 0.25s;

      & + li {
        margin-top: 0.5em;
      }

      &:hover {
        border-color: #646cff;

        & > i {
          visibility: visible;
        }
      }

      &.done {
        outline: 2px auto #ccc;

        & > span {
          text-decoration: line-through;
          opacity: 0.4;
        }
      }

      & > i {
        color: #999;
        font-size: 2em;
        font-style: normal;
        display: inline-block;
        width: 1em;
        height: 1em;
        line-height: 1em;
        text-align: center;
        visibility: hidden;
        position: absolute;
        top: 0;
        right: 0;
        transform: rotate(45deg);

        &:hover {
          color: #fd0000;
        }
      }
    }
  }

  @media screen and (max-width: 992px) {
    .todolist > li > i {
      visibility: visible;
    }
  }
</style>
