<script>
  const days = ['01'];
</script>

<h1>Maddy's Advent of Code 2025 Solutions</h1>

<ul>
  {#each days as day (day)}
    <!-- eslint-disable-next-line svelte/no-navigation-without-resolve -->
    <li><a href={`/day${day}`}>Day {day}</a></li>
  {/each}
</ul>
