<script lang="ts">
    let { onclick } = $props();

    function write(e: Event) {
        if (e === null)
            return;

        onclick(e?.target?.dataset.value);
    }

    $effect(() => {
        const buttons = document.querySelectorAll("div.button");
        for (let button of buttons) {
            button?.addEventListener("click", (e: Event) => { write(e) });
        }

        return () => {
            for (let button of buttons) {
                button?.removeEventListener("click", (e: Event) => { write(e) });
            }
        }
    });
</script>

<div class="buttons">
    <div class="button clear" data-value="C">C</div>
    <div class="button backspace" data-value="backspace">←</div>
    <div class="button operator" data-value="/">/</div>
    <div class="button operator" data-value="*">*</div>

    <div class="button" data-value="7">7</div>
    <div class="button" data-value="8">8</div>
    <div class="button" data-value="9">9</div>
    <div class="button operator" data-value="-">-</div>

    <div class="button" data-value="4">4</div>
    <div class="button" data-value="5">5</div>
    <div class="button" data-value="6">6</div>
    <div class="button operator" data-value="+">+</div>

    <div class="button" data-value="1">1</div>
    <div class="button" data-value="2">2</div>
    <div class="button" data-value="3">3</div>
    <div class="button" data-value="0">0</div>

    <div class="button" data-value=".">.</div>
    <div class="button equals" data-value="=">=</div>
</div>