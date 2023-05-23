<script>
  import { Link } from 'svelte-navigator';  
  import { Styles, Navbar, NavbarBrand, Nav, NavItem, NavLink  } from 'sveltestrap';
</script>

<Styles />

  <Navbar
    color="success"
  >
    <NavbarBrand href="/"><div class="linker">POC</div></NavbarBrand>
    <Nav>
      <NavItem>
        <NavLink href="#"><Link to="quiz"><div class="linker">Quiz</div></Link></NavLink>
      </NavItem>
      <NavItem>
        <NavLink href="#"><Link to="report"><div class="linker">Report</div></Link></NavLink>
      </NavItem>
    </Nav>

  </Navbar>


<header>
</header>

<style>
.linker{
   color:white;
}
</style>