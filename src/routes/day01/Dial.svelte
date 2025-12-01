<script lang="ts">
  type Props = {
    rotation: number
    stationary: boolean
  }

  let { rotation, stationary }: Props = $props();

  const stationaryColor = '#FFAAAA';
  const zeroColor = '#AAAAFF';

  let color = $derived(
    rotation === 0
    ? stationary ? stationaryColor : zeroColor
    : "#000000");
</script>

<svg viewBox="0 0 200 200" style:--r={`${rotation / 100 * 360}deg`}>
	<circle cx="100" cy="100" r="100" fill={color}/>
	<circle cx="100" cy="30" r="20" fill="white"/>
</svg>

<style>
  svg {
    max-width: 200px;
    rotate: var(--r)
  }
</style>
