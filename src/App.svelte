<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Svelte Sandbox</title>

    <!-- stylesheets -->
    <!-- link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.1/css/bulma.min.css" -->

  </head>
  <body>

    <h1 id="title-text">Svelte Sandbox</h1>

  <script>
    let itemDeletePanelIndex = undefined;
    let newItemDescription = '';
    let items = [
      {description: 'Take out garbage'},
      {description: 'Feed cat'}
    ];
    
    let currentlyHoveredItem = undefined;

    function itemCreate(description) {
      
      if (!newItemDescription) return false;
      
      let a, b;
      
      let newItem = {
        id: items.length,
        description
      }
      items = [...items, newItem];
      newItemDescription = '';
    }
    
    function itemDeletePanelToggle(index) {
      console.log('itemDeletePanelToggle()');
      if (itemDeletePanelIndex === index) {
        itemDeletePanelIndex = undefined;
      } else {
        itemDeletePanelIndex = index;
      }
    }
    
    const itemDelete = (index) => {
      console.log(index)
      items.splice(index, 1);
      items = items;
    }
  </script>

  <h2>
    To-Do List
  </h2>

  <input type="text"
         bind:value="{newItemDescription}"
         on:keyup="{e => e.key === 'Enter' && itemCreate(newItemDescription)}">
  <button on:click="{() => itemCreate(newItemDescription)}">
    Create new item
  </button>

  {#if items.length}
  <ol>
    {#each items as item, index}
      <li class="cursor-url">
        <span class="list-item-description"
              on:click="{() => itemDeletePanelToggle(index)}">
          {item.description}
        </span>
        
      {#if itemDeletePanelIndex === index}
        <span on:click="{() => itemDelete(index)}">&#x1f5d1</span>
      {/if}
        
    </li>
    {/each}
  </ol>
  {/if}

  <style>
    .list-item-description {
      font-weight: bold;
    }
      
    .cursor-url {
      cursor: pointer;
    }
  </style>       
     
  </body>
</html>

