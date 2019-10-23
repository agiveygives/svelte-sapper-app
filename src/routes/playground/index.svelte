<script>
  import SideDrawer from '../../components/sideDrawer/sideDrawer.svelte'

  const sections = [
    {
      name: 'Table',
      route: '/playground/table',
      indent: 0
    }
  ];
</script>

<div>
  <SideDrawer drawerItems={sections}>
    <h3>Andrew Givens</h3>
  </SideDrawer>
</div>
