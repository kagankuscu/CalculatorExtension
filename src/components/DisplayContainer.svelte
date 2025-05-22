<script lang="ts">
    let { expression = null, currentInput = "0" } = $props();
</script>

<div class="display-container">
    <div class="expression-display" id="expressionDisplay">{expression}</div>
    <div class="main-display" id="mainDisplay">{currentInput}</div>
</div>