<script>
    import Button from '@smui/button';
</script>
<style>
    nav {
        height: 10vh;
        background: #000000;
        font-family: sans-serif;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .logo {
        color: white;
        text-decoration: none;
        font-size: 16px;
        padding: 0 5%;
    }

    * :global(.signup-btn) {
        margin: 0;
    }

    .signup-btn-container {
        padding: 0 5%;
    }

</style>

<nav>
    <a href="#" class="logo">Ace Detective</a>
    <div class="signup-btn-container">
        <Button on:click={() => alert('Clicked!')} variant="unelevated" class="signup-btn">Sign Up</Button>
    </div>
</nav>