<script>
  import { sources } from "./sources.js";
  import Card from "./Card.svelte";
  import { onMount } from "svelte";

  let checked;
  console.log("checked=" + checked);
  let entries;
  let list = [];
  $: entries = list;

  function pushValues(event) {
    entries = [...entries, event.detail].filter(function(item, pos, self) {
      return self.indexOf(item) == pos;
    });
  }
  function removeValues(event) {
    // const index = entries.indexOf(event.detail);
    // console.log("now index of is:"+index)
    // entries.splice(index,1)
    // console.log("now list is:"+entries)
    entries = entries.filter(m => m !== event.detail);
  }

  $: console.log("mylist:" + entries);
</script>

<style>
  h1{
    padding:0 1em;
  }
  h2.selected {
    margin: 0;
    padding: 10px 5px 060px;
    position: fixed;
    top: 0;
    background: #dadada;
    font-size: 1.4em;
    width: 290px;
    border-bottom: 1px solid #fff;
  }
  ul {
    list-style: none;
    margin: 100px 0;
    padding: 0;
  }
  li {
    padding: 10px 10px;
    border-bottom: 1px solid #fff;
    display: flex;
    align-items: center;
  }
  li span {
    margin: 0 5px;
  }
  .aside {
    scroll-behavior: auto;
    width: 300px;
    height: 100vh;
    position: fixed;
    background: #dadada;
    border-right: 1px solid grey;
    top: 0;
    left: 0;
    overflow:auto;
  }
.container{
	margin:0 0 0 300px;
}
  .grid-container {
    padding:20px;
    
  }
  .grid {
    position: static;

    display: grid;
    grid-column-gap: 20px;
    grid-row-gap: 25px;

    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  }
  .submit{
    position: fixed;
    top:50px;
    left: 5px;
    z-index: 1;
  }
</style>

<main>

    <div class="container">
    	<h1>Γιωργος & Φωτεινή</h1>
	
	    <div class="grid-container">
	      <form action="" name="selection" id="selection" method="POST">
	        <div class="grid">
	          {#each sources as source, i}
	            <Card
	              on:add={pushValues}
	              on:remove={removeValues}
	              src={source.src}
	              name={'photo' + i} />
	          {/each}
	        </div>
	        <input type="submit" value="send selection!" class="submit" />
	      </form>
	
	    </div>
    </div>
    <div class="aside">
      <ul>
        <h2 class="selected">Selected Photos {entries.length} / 100</h2>
        {#each entries as item, i}
          <li>
            <span>{"#" + (i+1)}</span>
            <img src={item} alt="img-thumb" width="65" />
            <span>{' ' + item.substring(13)}</span>
          </li>
        {/each}
      </ul>
    </div>

  

</main>

