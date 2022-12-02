<script defer type="module" src="../svelteScripts/managers"></script>
<h2>If you're a manager and can't login contact Elo on Slack</h2>

{#if !signedIn}
    <form on:submit|preventDefault={login}>
        <div>
            <label for="username">Username</label>
            <input name="username" type="text" placeholder="colbernie">
        </div>
        <div>
            <label for="password">Password</label>
            <input name="password" type="text" placeholder="cynthiagang">    
        </div>
        <button type="submit">Login</button>
    </form>
{:else}
    <ManagerControlPanel></ManagerControlPanel>>
{/if}
