<script lang="ts">
    let { result = "0", currentInput = "0" } = $props();
</script>

<div class="display-container">
    <div class="expression-display" id="expressionDisplay">{result}</div>
    <div class="main-display" id="mainDisplay">{currentInput}</div>
</div>