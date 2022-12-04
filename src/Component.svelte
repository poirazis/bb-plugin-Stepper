<script>
  import "@spectrum-css/steplist"

  import { getContext, onMount } from "svelte"

  export let noSteps = 4
  export let activeStep = 2
  export let variant


  let steps = []
  let validProps = false;
  
  const { styleable } = getContext("sdk")
  const component = getContext("component")

  $: validProps = !isNaN(noSteps) && !isNaN(activeStep)
  $: steps.length = noSteps > -1 ? noSteps : 0
  $: activeStep = activeStep > 0 && activeStep <= noSteps ? activeStep : 1

</script>

<div use:styleable={$component.styles}>

  {#if validProps}
     
    <div class="spectrum-Steplist " role="list">

    {#each steps as step, i}
      <div 
        class="spectrum-Steplist-item" 
        class:u-tooltip-showOnHover = {variant === "withtooltip"}
        class:is-complete={ i < activeStep }
        role="listitem" aria-posinset="1" aria-setsize="4"> 
          {#if variant === "withlabel"}
            <span class="spectrum-Steplist-label">Step {i+1}</span>
          {/if}
          <span class="spectrum-Steplist-markerContainer">
            {#if variant === "withtooltip"}
            <div class="spectrum-Tooltip spectrum-Tooltip--top">
              <span class="spectrum-Tooltip-label">Step {i+1}</span>
              <span class="spectrum-Tooltip-tip"></span>
            </div>
            {/if}
            <span class="spectrum-Steplist-marker"></span>
          </span>
          <span class="spectrum-Steplist-segment"></span>
      </div>     
    {/each}

    </div>
  {:else}
    <p> Invalid Props ! </p>
  {/if}
</div>
