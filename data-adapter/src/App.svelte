<script>
  import { DataAdapter } from "./helpers/data-adapter.ts"

  let userInput = "";

  let markdown = ""
  async function handleInput(userInput) {
    const tP = new DataAdapter();

    const result = await tP.getQAPairsFromFFCContent(undefined, userInput)
    markdown = tP.getMarkdownFromQAPairs(result);
    console.log(markdown);
      // Deno.writeTextFile("./hello.md", markdown);
  }
</script>

<p>
  Enter a link to an ffc deck file here - e.g. "https://raw.githubusercontent.com/fancy-flashcard/deck-collection/main/wirtschaftsinformatik/Finanzbuchhaltung.json"
</p>
<p></p>
<!-- svelte-ignore a11y-autofocus -->
<input
  bind:value={userInput}
  on:keyup={(e) => e.key === "Enter" && handleInput(userInput)}
  type="text"
  name=""
  id=""
  autofocus
/>

<button on:click={() => handleInput(userInput)}>Convert To Markdown</button>

<p></p>
<textarea bind:value={markdown} name="" id="" cols="30" rows="10" />

<style>
  input {
    min-width: 100%
  }
  textarea {
    min-width: 100%;
    min-height: 80%
  }
</style>
