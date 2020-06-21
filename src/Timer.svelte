<script>
import { createEventDispatcher} from 'svelte';
 import ProgressBar from './ProgressBar.svelte';

const totalSeconds = 20;

let secondLeft = totalSeconds;
let isRunning = false;
let buttonText = "Iniciar";

$: progress = (totalSeconds - secondLeft) / totalSeconds * 100;

const dispatch = createEventDispatcher();

function startTimer() {
     isRunning = true;
     buttonText = "Lavando manos...";
const timer = setInterval(() => {
    secondLeft -= 1;
    if(secondLeft==0){
        clearInterval(timer);
        isRunning = false;
        buttonText = "Re Iniciar";
        secondLeft = totalSeconds;
        dispatch('end');
    }
}, 1000);

}


    
    



</script>


<div bp="grid">

<h2 bp="offset-5@md 4@md 12@sm">Seconds Left: {secondLeft}</h2>

</div>

<ProgressBar {progress} />

<div bp="grid">
<button disabled={isRunning} on:click={startTimer} bp="offset-5@md 4@md 12@sm" class="start">{buttonText}</button>
</div>

<style>
 .start{
background-color:rgb(154,73,73);
width:100%;
margin:10px 0px;
 }
 .start[disabled]{
background-color: rgb(194,194,194);
cursor: not-allowed;
 }
</style>
