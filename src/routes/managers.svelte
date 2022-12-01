<script type="ts" context="module">
    let data: any;
    let signedIn = false;
    export let departmentSignedIn;
    export function getResponseData(file: string) : Promise<any> {
      if(typeof(data) === "undefined") {
            fetch(file)
            .then(res => {
                data = res.json();
                return data;
            }).catch(this.handleError);
      } else {
            return Promise.resolve(data);
      }
    }


    function login(event: SubmitEvent & { currentTarget: EventTarget & HTMLFormElement; }) {
        let formData = new FormData(this);

        const password = formData.get("password").toString();
        const username = formData.get("username").toString();

        let data = getResponseData("../secrets/managers.json");

        if(data.hasOwnProperty(username)){
            if(data[username]["password"] == password){
                departmentSignedIn = data[username]["department"];
                signedIn = true;
                console.log(`Logged in ${username} for department ${departmentSignedIn}`)
            }
        }
    }
</script>
    


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
    
{/if}