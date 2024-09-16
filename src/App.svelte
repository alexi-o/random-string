<script>
  let randomString = "";

  function generateRandomString(length = 8) {
    const characters =
      "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
    let result = "";
    for (let i = 0; i < length; i++) {
      result += characters.charAt(
        Math.floor(Math.random() * characters.length)
      );
    }
    randomString = result;
  }
</script>

<main>
  <h1>Random String Generator</h1>
  <button on:click={() => generateRandomString(16)}>Generate String</button>
  <p>{randomString}</p>
</main>

<style>
  main {
    text-align: center;
    padding: 20px;
  }

  button {
    margin-top: 20px;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 16px;
  }

  p {
    margin-top: 20px;
    font-size: 18px;
    word-break: break-all;
  }
</style>
