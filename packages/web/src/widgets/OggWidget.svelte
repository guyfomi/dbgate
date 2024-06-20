<script lang="ts">
  import _ from 'lodash';
    
  import WidgetColumnBar from './WidgetColumnBar.svelte';
  import WidgetColumnBarItem from './WidgetColumnBarItem.svelte';
  import WidgetsInnerContainer from './WidgetsInnerContainer.svelte';
  import OggProcs from './OggProcs.svelte';
  import OggCaptureLag from './OggCaptureLag.svelte';
  import OggPropagationLag from './OggPropagationLag.svelte';
  import OggReplicatLag from './OggReplicatLag.svelte';

</script>

<WidgetColumnBar>
  <WidgetColumnBarItem title="Etat des Processus" name="processStates" storageName='processWidget' height="25%">
    <WidgetsInnerContainer>
      <OggProcs/>
    </WidgetsInnerContainer>
  </WidgetColumnBarItem>  
  <WidgetColumnBarItem title="Latence Capture" name="captureLag" storageName='captureLagChartd' height="25%">
    <WidgetsInnerContainer>
      <OggCaptureLag/>
    </WidgetsInnerContainer>
  </WidgetColumnBarItem>
  <WidgetColumnBarItem title="Latence Propagation" name="datapumpLag" storageName='datapumpLagChartd' height="25%">
    <WidgetsInnerContainer>
      <OggPropagationLag/>
    </WidgetsInnerContainer>
  </WidgetColumnBarItem>
  <WidgetColumnBarItem title="Latence Replication" name="replicatLag" storageName='replicatLagChartd' height="25%">
    <WidgetsInnerContainer>
      <OggReplicatLag/>
    </WidgetsInnerContainer>
  </WidgetColumnBarItem>
</WidgetColumnBar>