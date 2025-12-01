<script>
    import { resolve } from "$app/paths";

  const days = ['01'];
</script>

<h1>Maddy's Advent of Code 2025 Solutions</h1>

<ul>
  {#each days as day (day)}
    <!--
      This is really fugly to hard-code it to make it work in deployment, but I simply
      do not have the energy to figure out how to make this work nicely when it isn't
      at the root of the domain.
    -->
    <li><a href="/aoc-2025/day01">Day {day}</a></li>
  {/each}
</ul>
