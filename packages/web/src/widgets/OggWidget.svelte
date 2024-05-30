<script lang="ts">
  import _ from 'lodash';
    
  import WidgetColumnBar from './WidgetColumnBar.svelte';
  import WidgetColumnBarItem from './WidgetColumnBarItem.svelte';
  import WidgetsInnerContainer from './WidgetsInnerContainer.svelte';
  import OggProcs from './OggProcs.svelte';

</script>

<WidgetColumnBar>
  <WidgetColumnBarItem title="Etat des Processus" name="processStates" storageName='processWidget'>
    <WidgetsInnerContainer>
      <OggProcs/>
    </WidgetsInnerContainer>
  </WidgetColumnBarItem>  
</WidgetColumnBar>
