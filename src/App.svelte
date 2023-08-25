<script>
  const triggerFileInput = () => {
    document.getElementById("csv-input")?.click();
  };

  let imageUrl = "./contact-photo.png" || null;

  const uploadData = (event) => {
    let file = event.target?.files?.[0];

    imageUrl = URL.createObjectURL(file);
  };

  let margin = 0;
  let columns = 6;
  let rows = 6;
  $: mainStyles = `
    --margin: ${margin}%;
    --columns: repeat(${columns}, 1fr);
    --rows: repeat(${rows}, 1fr);
  `;

  const cropImages = () => {
    console.log("cropImages");
  };

  const previewGif = () => {
    console.log("previewGif");
  };

  const exportImages = () => {
    console.log("exportImages");
  };

  const exportGif = () => {
    console.log("exportGif");
  };
</script>

<aside>
  <section>
    <h2>Contact Sheet Tool</h2>
    <p>
      Curabitur urna dolor, ullamcorper a fringilla in, varius et mi. Donec quis
      leo tristique, auctor ex ut, dictum lorem. Built by <a
        href="https://www.romellogoodman.com/">Romello Goodman</a
      >
      and
      <a href="https://zinehug.com/">Zine Hug</a>.
    </p>
  </section>
  <section>
    <h4>Upload</h4>
    <input id="csv-input" type="file" on:change={uploadData} />
    <button on:click={triggerFileInput}>Upload Photo</button>
  </section>
  <section>
    <h4>Edit</h4>
    <div class="control">
      <label for="margin">Margin</label>
      <input id="margin" type="range" min="0" max="30" bind:value={margin} />
    </div>
    <div class="control">
      <label for="columns">Columns</label>
      <input id="columns" type="range" min="2" max="8" bind:value={columns} />
    </div>
    <div class="control">
      <label for="rows">Rows</label>
      <input id="rows" type="range" min="2" max="8" bind:value={rows} />
    </div>
    <button on:click={cropImages}>Crop Images</button>
    <button on:click={previewGif}>Preview Animation</button>
  </section>
  <section>
    <h4>Export</h4>
    <button on:click={exportImages}>Cropped Images</button>
    <button on:click={exportGif}>GIF Animation</button>
  </section>
</aside>
<main style={mainStyles}>
  {#if imageUrl}
    <div class="contact-sheet-overlap">
      <div class="grid-preview">
        {#each new Array(columns * rows).fill(null) as _, index}
          <div>
            <p class="number">{index + 1}</p>
          </div>
        {/each}
      </div>
      <img src={imageUrl} alt="The uploaded contact sheet." />
    </div>
  {/if}
</main>

<style lang="scss">
  :global(#app) {
    width: 100%;
    display: flex;
  }

  aside,
  main {
    height: 100vh;
  }

  aside {
    overflow: scroll;
    flex-basis: 300px;
    padding: 0px 16px;
  }

  section {
    margin: 16px 0px;

    h4 {
      margin-bottom: 8px;
    }

    p {
      margin-bottom: 4px;
    }

    .control {
      display: flex;
      margin-bottom: 4px;

      label {
        flex-basis: 100px;
      }

      input {
        flex-grow: 1;
      }
    }

    input[type="file"] {
      display: none;
    }

    button {
      width: 100%;
      margin: 8px 0px;
    }
  }

  main {
    overflow: hidden;
    flex-grow: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 32px;
    background-color: #eee;
    position: relative;
  }

  .contact-sheet-overlap {
    position: relative;
    background-color: red;
  }

  img {
    max-width: 100%;
    max-height: 100%;
    margin: auto;
  }

  .grid-preview {
    position: absolute;
    top: 0px;
    left: 0px;
    width: 100%;
    height: 100%;
    display: grid;
    grid-template-rows: var(--rows);
    grid-template-columns: var(--columns);
    padding: var(--margin);
    border: 1px solid var(--color);
    color: var(--color);
    font-weight: bold;

    div {
      display: flex;
      padding: 8px;
      font-weight: bold;
      align-items: end;
      justify-content: end;
      background-color: rgba(255, 255, 255, 0.2);
      border: 2px solid var(--color);
    }
  }
</style>
