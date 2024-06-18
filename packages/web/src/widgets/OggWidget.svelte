<script lang="ts">
  import _ from 'lodash';
    
  import WidgetColumnBar from './WidgetColumnBar.svelte';
  import WidgetColumnBarItem from './WidgetColumnBarItem.svelte';
  import WidgetsInnerContainer from './WidgetsInnerContainer.svelte';
  import OggProcs from './OggProcs.svelte';
  import OggCaptureLag from './OggCaptureLag.svelte';

</script>

<WidgetColumnBar>
  <WidgetColumnBarItem title="Etat des Processus" name="processStates" storageName='processWidget' height="25%">
    <WidgetsInnerContainer>
      <OggProcs/>
    </WidgetsInnerContainer>
  </WidgetColumnBarItem>  
  <WidgetColumnBarItem title="Latence Capture" name="captureLag" storageName='captureLagChartd' height="50%">
    <WidgetsInnerContainer>
      <OggCaptureLag/>
    </WidgetsInnerContainer>
  </WidgetColumnBarItem>
</WidgetColumnBar>