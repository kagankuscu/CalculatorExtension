
<script lang="ts">
	import { evaluate, string } from "mathjs";
	import ButtonContainer from "../components/ButtonContainer.svelte";
	import DisplayContainer from "../components/DisplayContainer.svelte";

    let result = $state("0");
    let currentInput = $state("0");
    let previousInput = "";
    let resultDisplayed = $state(false);
    let isDecimal = false;

    function onkeydown(event: KeyboardEvent | string) {
        let key: string = "";
        console.log(event.constructor)
        if (event instanceof KeyboardEvent)
            key = event.key;
        else if (typeof(event) === "string")
            key = event;

        if (previousInput === "" && "0" === key) {
            return;
        }

        if (previousInput === "" && ![".", ","].includes(key)) {
            currentInput = "";
        }

        if (resultDisplayed) {
            resetCalculator();
            return;
        }

        if (key >= "0" && key <= "9") {
            currentInput += key;
        } else if (["+", "-", "/", "*"].includes(key) && !["+", "-", "/", "*"].includes(currentInput.slice(-1))) {
            currentInput += key;
            isDecimal = false;
        } else if ("Enter" === key || "=" === key) {
            resultDisplayed = true;
            calculate();
        } else if ("Backspace" === key) {
            handleBackspace();
            return;
        } else if ("c" === key || "C" === key) {
            resetCalculator()
            return;
        } else if (("." === key || "," === key) && ![".", ","].includes(previousInput) && !isDecimal) {
            isDecimal = true;
            currentInput += ".";
            previousInput = ".";
        }

        previousInput = key;
    }

    function calculate() {
        result = evaluate(currentInput);
        updateDisplay();
    }

    function handleBackspace() {
        if (resultDisplayed) {
            resetCalculator();
            return;
        }

        if (!isDecimal) {
            isDecimal = false;
        }

        if (["+", "-", "/", "*"].includes(currentInput.slice(-1))) {
            const splitN = currentInput.split(/\+|-|\/|\*/);
            isDecimal = splitN[splitN.length - 2].includes(".");
            console.log(isDecimal);
        }

        if ("." === currentInput.slice(-1)) {
            isDecimal = false;
        }

        if (currentInput === "Error") {
            resetCalculator();
            return;
        }

        if (currentInput.length > 1) {
            currentInput = currentInput.slice(0, -1);
        } else {
            resetCalculator();
        }
    }

    function resetCalculator() {
        result = "0";
        currentInput = "0";
        resultDisplayed = false;
        previousInput = "";
        isDecimal = false;
    }

    function updateDisplay() {
        const empty = currentInput;
        currentInput = result;
        result = empty;

    }

</script>

<svelte:window {onkeydown} />

<div class="calculator">
    <DisplayContainer {currentInput} {result} />
    <ButtonContainer onclick={onkeydown} />
</div>