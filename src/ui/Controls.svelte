<script lang='ts'>
  import Checkbox from './controls/Checkbox.svelte'
  import Colours from './controls/Colours.svelte'
  import Number from './controls/Number.svelte'
  import Select from './controls/Select.svelte'
  import Size from './controls/Size.svelte'
  import StopConditions from './controls/StopConditions.svelte';
  import { hints } from './hints'
  import { scaleFrequencies, scaleRatios, spirals } from './select-options'

  export let disabled = false
  export let config
</script>

<template>
  <div class='section'>
    <Size bind:size={config.size} {disabled} />
  </div>
  <div class='section'>
    <Number
      {disabled}
      bind:value={config.start.count}
      hint={hints.startingCount}
      label='Starting count'
      min={1}
    />
    <Number
      {disabled}
      bind:value={config.start.size}
      hint={hints.startingSize}
      label='Starting scale'
      max={100}
      min={1}
      unit='%'
    />
  </div>
  <div class='section'>
    <Select
      {disabled}
      bind:value={config.scale.ratio}
      hint={hints.scaleRatio}
      label='Scaling ratio'
      options={scaleRatios}
    />
    <Select
      {disabled}
      bind:value={config.scale.frequency}
      hint={hints.scaleFrequency}
      label='Scale frequency'
      options={scaleFrequencies}
    />
    <Checkbox
      {disabled}
      bind:checked={config.scale.strictFrequency}
      hint={hints.strictFrequency}
      label='Enforce strict frequency counts'
    />
    <Number
      {disabled}
      bind:value={config.scale.maxLevels}
      hint={hints.maxScaleLevels}
      label='Maximum scaling levels'
      max={20}
      min={3}
    />
  </div>
  <div class='section'>
    <Number
      {disabled}
      bind:value={config.tile.padding}
      hint={hints.padding}
      label='Padding'
      min={0}
      unit='px'
    />
    <Number
      {disabled}
      bind:value={config.tile.rotation}
      hint={hints.rotation}
      label='Rotation increment'
      min={1}
      max={360}
      unit='°'
    />
    <Number
      {disabled}
      bind:value={config.tile.wiggle}
      hint={hints.wiggle}
      label='Wiggle'
      min={0}
      max={50}
    />
  </div>

  <div class='section'>
    <Colours colours={config.colours} />
  </div>

  <div class='section'>
    <Select
      {disabled}
      bind:value={config.spiral}
      hint={hints.spiral}
      label='Spiral'
      options={spirals}
    />
    <Checkbox
      {disabled}
      bind:checked={config.twoPass}
      hint={hints.twoPass}
      label='Resize placed tiles'
    />
    <Checkbox
      {disabled}
      bind:checked={config.debug}
      hint={hints.debug}
      label='Debug collisions'
    />
  </div>

  <div class='section'>
    <StopConditions
      {disabled}
      bind:maxTiles={config.stopConditions.tiles}
      bind:maxTime={config.stopConditions.time}
    />
  </div>
</template>
