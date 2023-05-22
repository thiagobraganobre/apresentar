<script>
  import { Link } from 'svelte-navigator';
</script>


<header>
  <nav>
    <Link to="quiz">Quiz</Link>
    <Link to="report">Report</Link>
  </nav>
</header>


<style>
  header {
    background: #eeeeee;
    width: 100%;
    margin: 20px auto;
    padding: 20px;
    max-width: 1024px;
  }
</style>
