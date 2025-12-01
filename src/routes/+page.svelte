<script>
    import { resolve } from "$app/paths";

  const days = ['01'];
</script>

<h1>Maddy's Advent of Code 2025 Solutions</h1>

<ul>
  {#each days as day (day)}
    <li><a href={resolve(`/day01`)}>Day {day}</a></li>
  {/each}
</ul>
