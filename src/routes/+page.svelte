
<script lang="ts">
	import ButtonContainer from "../components/ButtonContainer.svelte";
	import DisplayContainer from "../components/DisplayContainer.svelte";

    let expression = $state("");
    let currentInput = $state("0");

    function onkeydown(event: KeyboardEvent) {
        const key = event.key;
        currentInput += key;
    }
</script>

<svelte:window {onkeydown} />

<div class="calculator">
    <DisplayContainer {currentInput}/>
    <ButtonContainer />
</div>