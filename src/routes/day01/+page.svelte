<script lang="ts">
  import Dial from "./Dial.svelte";

  const sleep = (ms: number) => new Promise(r => (void setTimeout(r, ms)));

  let input = $state('');
  let speed = $state(0);
  let sleepTime = $derived(100 - speed);

  let active = $state(false);
  let stateMessage = $state('');
  let rotation = $state(50);
  let stationary = $state(true);

  let resultPart1 = $state(0);
  let resultPart2 = $state(0);

  async function applyRotation(command: string) {
    let direction = command[0] === "R" ? 1 : -1;
    let amount = parseInt(command.slice(1));
    stationary = false;

    for (let i = 0; i < amount; i++) {
      rotation = (rotation + direction) % 100;
      if (rotation === 0) {
        resultPart2++;
      }
      stateMessage = `${command[0]}: ${i}/${amount}`;
      if (sleepTime) await sleep(sleepTime);
    }

    stationary = true;
  }

  async function execute() {
    active = true;
    resultPart1 = 0;
    resultPart2 = 0;

    for (const line of input.split('\n')) {
      await applyRotation(line);
      if (rotation === 0) {
        resultPart1++;
      }
      await sleep(sleepTime * 10);
    }

    active = false;
  }
</script>


<main>
  <div id="in">
    <h1>Day 1</h1>
    <textarea bind:value={input}></textarea>
    <button onclick={execute} disabled={active}>Execute</button>
    <div>
      <em>Speed</em>
      <input type="range" min={0} max={100} bind:value={speed}>
    </div>
  </div>
  <div id="display">
    {#if active}
      <p>{stateMessage}</p>
    {:else}
      <p>Idle</p>
    {/if}
    <p>Part 1: {resultPart1}, Part 2: {resultPart2}</p>

    <Dial {rotation} {stationary} />
  </div>
</main>

<style>
  main {
    display: flex;
    width: 100%;
    gap: 20px;
  }
  main > div {
    width: 100%;
    margin: 10px;
  }

  textarea {
    width: 100%;
    height: 100%;
  }
</style>
