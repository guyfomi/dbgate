<script>
  function openTab(evt, cityName) {
    console.log('clicked ....');
    console.dir(evt);
    // Declare all variables
    var i, tabcontent, tablinks;

    // Get all elements with class="tabcontent" and hide them
    tabcontent = document.getElementsByClassName('tabcontent');
    for (i = 0; i < tabcontent.length; i++) {
      tabcontent[i].style.display = 'none';
    }

    // Get all elements with class="tablinks" and remove the class "active"
    tablinks = document.getElementsByClassName('tablinks');
    for (i = 0; i < tablinks.length; i++) {
      tablinks[i].className = tablinks[i].className.replace(' active', '');
    }

    // Show the current tab, and add an "active" class to the button that opened the tab
    document.getElementById(cityName).style.display = 'block';
    evt.currentTarget.className += ' active';
  }
</script>

<!-- Tab links -->

<div class="tab">
  <button class="tablinks" on:click={() => openTab(event, "Capture")}>Capture</button>
  <button class="tablinks" on:click={() => openTab(event, "Propagation")}>Propagation</button>
  <button class="tablinks" on:click={() => openTab(event, "Replication")}>Replication</button>
</div>

<!-- Tab content -->
<div id="Capture" class="tabcontent">
  <h3>London</h3>
  <p>London is the capital city of England.</p>
</div>

<div id="Propagation" class="tabcontent">
  <h3>Paris</h3>
  <p>Paris is the capital of France.</p>
</div>

<div id="Replication" class="tabcontent">
  <h3>Tokyo</h3>
  <p>Tokyo is the capital of Japan.</p>
</div>

<style>
body {font-family: Arial;}

/* Style the tab */
.tab {
  overflow: hidden;
  border: 1px solid #ccc;
  background-color: #f1f1f1;
}

/* Style the buttons inside the tab */
.tab button {
  background-color: inherit;
  float: left;
  border: none;
  outline: none;
  cursor: pointer;
  padding: 14px 16px;
  transition: 0.3s;
  font-size: 17px;
}

  /* Change background color of buttons on hover */
  .tab button:hover {
    background-color: #ddd;
  }

  /* Create an active/current tablink class */
  .tab button.active {
    background-color: #ccc;
  }

  /* Style the tab content */
  .tabcontent {
    display: none;
    padding: 6px 12px;
    border: 1px solid #ccc;
    border-top: none;
  }

  .tabcontent {
    animation: fadeEffect 1s; /* Fading effect takes 1 second */
  }

  /* Go from zero to full opacity */
  @keyframes fadeEffect {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>