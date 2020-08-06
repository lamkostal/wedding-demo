<script>
import {createEventDispatcher} from "svelte";
const dispatch = new createEventDispatcher();


 
export let src,name
let checked = false;
let checks
$: checks=!checked


function sendMessage(){
S: console.log("checks from comp:"+" "+ checks)

    if(checks){dispatch('add',this.value)
    console.log("adds")}
    else{
        dispatch('remove',this.value)
        console.log("removes")
        }

}
S: console.log("checked from comp:"+" "+ checked)
// S: console.log("checks from comp:"+" "+ checks)



</script>

<div class="card">
  
  <input class="checkbox" type="checkbox" name={name} bind:checked={checked} on:input={sendMessage} value="{src}">
  
 
  <img src="{src}" alt="" class="photo">
  <span class="file-name">{src.substring(13)}</span>
    
</div>

<style>
.photo{
    width:100%;
    padding: 0px;
    transition:0.2s ease;
    border-radius: 2px;
}
.file-name{
    position: relative;
    padding: 5px;
    
}
.checkbox:checked + img{
    background: green;
    padding: 5px;

}
.checkbox{
    -webkit-appearance: none;
    border: 1px solid #636363;
	box-shadow: 0 1px 2px rgba(0,0,0,0.1), inset 0px -15px 10px -12px rgba(0,0,0,0.05);
	padding: 9px;
	border-radius: 3px;
	display: inline-block;
    position: relative;
    margin: 0;
   
}
.checkbox:checked {
    background: green;
    border: 1px solid #acacac;
    outline:none;

}
.checkbox:active, .checkbox:focus{
     outline:none;
}
.checkbox:checked:after {
	content: '\2714';
	font-size: 14px;
	position: absolute;
	top: 0px;
	left: 3px;
	color: #ffffff;
}
</style>