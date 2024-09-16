<script>
  let randomStrings = [];
  let stringLength = 28;
  let numberOfOutputs = 5;
  let includeLowercase = true;
  let includeUppercase = true;
  let includeNumbers = true;
  let includeSpecialCharacters = false;
  let copyMessage = "";
  let themeColor = "#51bf37";

  function generateRandomStrings() {
    let characters = "";
    if (includeLowercase) characters += "abcdefghijklmnopqrstuvwxyz";
    if (includeUppercase) characters += "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    if (includeNumbers) characters += "0123456789";
    if (includeSpecialCharacters) characters += "!@#$%^&*_?";

    if (!characters) {
      randomStrings = ["Select at least one character set option"];
      return;
    }

    randomStrings = [];

    for (let j = 0; j < numberOfOutputs; j++) {
      let result = "";
      for (let i = 0; i < stringLength; i++) {
        result += characters.charAt(
          Math.floor(Math.random() * characters.length)
        );
      }
      randomStrings.push(result);
    }
  }

  function setNumberOfOutputs(count) {
    numberOfOutputs = count;
  }

  async function copyToClipboard(text) {
    try {
      await navigator.clipboard.writeText(text);
      copyMessage = "Copied to clipboard!";
      setTimeout(() => {
        copyMessage = "";
      }, 1000);
    } catch (err) {
      copyMessage = "Failed to copy!";
    }
  }

  function setThemeColor(color) {
    themeColor = color;
  }
</script>

<main style="--theme-color: {themeColor}">
  <div class="terminal-header">
    <div class="buttons">
      <button class="button red" on:click={() => setThemeColor("#ff5f56")}
      ></button>
      <button class="button yellow" on:click={() => setThemeColor("#ffbd2e")}
      ></button>
      <button class="button green" on:click={() => setThemeColor("#51bf37")}
      ></button>
    </div>

    <div class="title">Random String Generator</div>
  </div>

  <div class="terminal-body">
    <div class="input-container">
      <label for="stringLength">Length:</label>
      <div class="range-container">
        <input
          id="stringLength"
          type="number"
          min="1"
          max="128"
          bind:value={stringLength}
        />
        <input
          type="range"
          min="1"
          max="128"
          bind:value={stringLength}
          class="slider"
        />
      </div>
    </div>

    <div class="input-container">
      <!-- svelte-ignore a11y-label-has-associated-control -->
      <label>Outputs:</label>
      <div class="button-group">
        <button
          on:click={() => setNumberOfOutputs(1)}
          class:numberSelected={numberOfOutputs === 1}>1</button
        >
        <button
          on:click={() => setNumberOfOutputs(5)}
          class:numberSelected={numberOfOutputs === 5}>5</button
        >
        <button
          on:click={() => setNumberOfOutputs(10)}
          class:numberSelected={numberOfOutputs === 10}>10</button
        >
        <button
          on:click={() => setNumberOfOutputs(25)}
          class:numberSelected={numberOfOutputs === 25}>25</button
        >
      </div>
    </div>

    <div class="input-container">
      <!-- svelte-ignore a11y-label-has-associated-control -->
      <label>Options:</label>
      <div class="checkbox-group">
        <label>
          <input type="checkbox" bind:checked={includeLowercase} /> Lowercase
        </label>
        <label>
          <input type="checkbox" bind:checked={includeUppercase} /> Uppercase
        </label>
        <label>
          <input type="checkbox" bind:checked={includeNumbers} /> Numbers
        </label>
        <label>
          <input type="checkbox" bind:checked={includeSpecialCharacters} /> Special
        </label>
      </div>
    </div>

    <button on:click={generateRandomStrings}>Generate Strings</button>

    <ul>
      {#each randomStrings as string, index}
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
        <li class="random-string" on:click={() => copyToClipboard(string)}>
          {string}
        </li>
      {/each}
    </ul>
    {#if copyMessage}
      <div class="copy-message">{copyMessage}</div>
    {/if}
  </div>
</main>

<style>
  main {
    width: 400px;
    margin: 0 auto;
    border-radius: 5px;
    box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.3);
    overflow: hidden;
    font-family: "Courier New", Courier, monospace;
    background-color: #000000;
    color: var(--theme-color);
  }

  .terminal-header {
    display: flex;
    align-items: center;
    padding: 10px;
    background-color: #333;
  }

  .buttons {
    display: flex;
    gap: 5px;
  }

  .buttons .button {
    all: unset;
    display: inline-block;
    width: 12px;
    height: 12px;
    border-radius: 50%;
    cursor: pointer;
  }

  .button {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    display: inline-block;
  }

  .random-string {
    cursor: pointer;
  }

  .button.red {
    background-color: #ff5f56;
  }

  .button.yellow {
    background-color: #ffbd2e;
  }

  .button.green {
    background-color: #51bf37;
  }

  .title {
    flex-grow: 1;
    text-align: center;
    color: var(--theme-color);
    font-weight: bold;
    font-size: 14px;
  }

  .terminal-body {
    padding: 20px;
    background-color: #000000;
  }

  .input-container {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin-bottom: 20px;
    width: 300px;
  }

  label {
    font-size: 14px;
    color: var(--theme-color);
    margin-bottom: 5px;
  }

  .range-container {
    width: 100%;
  }

  input[type="number"] {
    width: 100%;
    padding: 5px;
    background-color: #333;
    color: var(--theme-color);
    border: 1px solid #555;
    border-radius: 4px;
    margin-bottom: 5px;
  }

  .slider {
    width: 100%;
    appearance: none;
    height: 8px;
    border-radius: 5px;
    background: var(--theme-color);
    outline: none;
    opacity: 0.7;
    transition: opacity 0.15s ease-in-out;
  }

  .slider:hover {
    opacity: 1;
  }

  .button-group {
    display: flex;
    gap: 10px;
  }

  .button-group button {
    padding: 5px 10px;
    background-color: #444;
    color: var(--theme-color);
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
  }

  .button-group button:hover {
    background-color: #555;
  }

  .button-group button.numberSelected {
    background-color: var(--theme-color);
    color: #000000;
  }

  .checkbox-group {
    display: flex;
    flex-direction: column;
    gap: 5px;
  }

  .checkbox-group label {
    display: flex;
    align-items: center;
    gap: 5px;
    color: var(--theme-color);
  }

  button {
    padding: 10px 20px;
    cursor: pointer;
    font-size: 14px;
    color: #000000;
    background-color: var(--theme-color);
    border: none;
    border-radius: 4px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.3);
    width: 100%;
  }

  ul {
    margin-top: 20px;
    list-style: none;
    padding: 0;
  }

  li {
    margin: 5px 0;
    padding: 5px;
    font-size: 14px;
    word-break: break-all;
    background-color: #262626;
    border-radius: 4px;
    color: var(--theme-color);
  }

  .copy-message {
    color: var(--theme-color);
    font-size: 14px;
    text-align: center;
  }
</style>
