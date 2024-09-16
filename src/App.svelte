<script>
  let randomStrings = [];
  let stringLength = 28;
  let numberOfOutputs = 5;

  function generateRandomStrings() {
    const characters =
      "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
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
</script>

<main>
  <div class="terminal-header">
    <div class="buttons">
      <span class="button red"></span>
      <span class="button yellow"></span>
      <span class="button green"></span>
    </div>
    <div class="title">Random String Generator</div>
  </div>

  <div class="terminal-body">
    <div class="input-container">
      <label for="stringLength">String Length:</label>
      <input
        id="stringLength"
        type="number"
        min="1"
        max="128"
        bind:value={stringLength}
      />
    </div>

    <div class="input-container">
      <label>Number of Outputs:</label>
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

    <button on:click={generateRandomStrings}>Generate Strings</button>

    <ul>
      {#each randomStrings as string, index}
        <li key={index}>{string}</li>
      {/each}
    </ul>
  </div>
</main>

<style>
  main {
    width: 600px;
    margin: 50px auto;
    border-radius: 5px;
    box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.3);
    overflow: hidden;
    font-family: "Courier New", Courier, monospace;
    background-color: #1e1e1e;
    color: #cccccc;
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

  .button {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    display: inline-block;
  }

  .button.red {
    background-color: #ff5f56;
  }

  .button.yellow {
    background-color: #ffbd2e;
  }

  .button.green {
    background-color: #27c93f;
  }

  .title {
    flex-grow: 1;
    text-align: center;
    color: #cccccc;
    font-weight: bold;
    font-size: 14px;
  }

  .terminal-body {
    padding: 20px;
    background-color: #1e1e1e;
  }

  .input-container {
    display: flex;
    align-items: center;
    margin: 10px 0;
  }

  label {
    width: 150px; /* Fixed width to align inputs */
    font-size: 14px;
    color: #888;
    margin-right: 10px;
  }

  input {
    flex: 1;
    padding: 5px;
    background-color: #333;
    color: #cccccc;
    border: 1px solid #555;
    border-radius: 4px;
  }

  .button-group {
    display: flex;
    gap: 10px;
  }

  .button-group button {
    padding: 5px 10px;
    background-color: #444;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
  }

  .button-group button:hover {
    background-color: #555;
  }

  .button-group button.numberSelected {
    background-color: #007acc;
    color: #ffffff;
  }

  button {
    margin-top: 20px;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 14px;
    color: #ffffff;
    background-color: #007acc;
    border: none;
    border-radius: 4px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.3);
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
    color: #9cdcfe;
  }
</style>
