<script>
  import { Router, Route } from 'svelte-navigator';
  import Header from './components/Header.svelte';
  import Footer from './components/Footer.svelte';

  import Quiz from './routes/Quiz.svelte';
  import Report from './routes/Report.svelte';
</script>


<Router>
  <Header />
  <main>
    <Route path="/">
      <Quiz />
    </Route>
    
    <Route path="quiz" component={Quiz} />
    <Route path="report" component={Report} />
  </main>
  <Footer />
</Router>


<style>
  main {
    width: 100%;
    margin: 0 auto;
    padding: 0 1rem;
    max-width: 1024px;
  }
</style>
