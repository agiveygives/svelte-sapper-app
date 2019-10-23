<script>
  export let drawerItems = [];

  import Drawer, {AppContent, Content, Header, Title, Subtitle, Scrim} from '@smui/drawer';
  import List, {Item, Text, Separator, Subheader} from '@smui/list';
  import {stores} from '@sapper/app';

  const {page} = stores();
  let mainContent;

  function pickSection(section) {
    mainContent.scrollTop = 0;

    // Svelte/Sapper is not updated the components correctly, so I need this.
    drawerItems.forEach(drawerItem => drawerItem.component.$set({activated: false}));
    section.component.$set({activated: true});
  }
</script>

<style>
  .drawer-container {
    flex-grow: 1;
    height: 100vh;
    display: flex;
  }
</style>

<div class="drawer-container">
  <Drawer>
    <Content>
      <List>
        {#each drawerItems as drawerItem}
          <Item
              bind:this={drawerItem.component}
              href={'route' in drawerItem ? drawerItem.route : drawerItem.shortcut}
              on:click={() => pickSection(drawerItem)}
              activated={'route' in drawerItem && drawerItem.route === $page.path}
              title={drawerItem.name}
              style="{drawerItem.indent ? 'margin-left: '+(drawerItem.indent * 25)+'px;' : ''}"
            >
              <Text class="mdc-theme--on-secondary">{drawerItem.name}</Text>
            </Item>
        {/each}
      </List>
    </Content>
  </Drawer>

  <AppContent class="app-content">
    <main class="main-content">
      <slot></slot>
    </main>
  </AppContent>
</div>