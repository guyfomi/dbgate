<script lang="ts">
  import _ from 'lodash';
    
  import WidgetColumnBar from './WidgetColumnBar.svelte';
  import WidgetColumnBarItem from './WidgetColumnBarItem.svelte';
  import WidgetsInnerContainer from './WidgetsInnerContainer.svelte';

</script>

<WidgetColumnBar>
  <WidgetColumnBarItem title="Etat des Processus" name="processStates" storageName='processWidget'>
    <WidgetsInnerContainer>
    
    </WidgetsInnerContainer>
  </WidgetColumnBarItem>  
</WidgetColumnBar>
