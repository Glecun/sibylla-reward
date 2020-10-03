<script>
   export let user;
   export let auth;

   let name;
   let editMode = false
   let displayName = user.displayName;

   function updateDisplayName(name) {
      user.updateProfile({displayName: name}).then(function() {
         displayName = user.displayName
      });
      editMode = false
   }
</script>

<main>
   <div>
      <span>Id : {user.uid}</span>
      {#if editMode}
         <span>
            <input placeholder="Nom" bind:value={name}>
            <button on:click={() => updateDisplayName(name)}>✔️</button>
         </span>
      {:else}
         <span>
            <span>Nom : {displayName}</span>
            <button class="edit" on:click={() => editMode = true}>🖊️</button>
         </span>

      {/if}

   </div>
   <button class="disconnect" on:click={() => auth.signOut()}>Déconnexion</button>
</main>

<style>
   main {
      display: flex;
      flex-direction: column;
      box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
      border: 1px solid black;
      width: 80vw;
      padding: 20px;
   }

   div {
      display: flex;
      flex-direction: column;
   }

   button.disconnect {
      margin-top: 10px;
      width: 120px;
      align-self: flex-end;
   }

   button.edit {
      margin: 0;
      padding: 2px;
      font-size: 14px;
      margin-left: 7px;
   }
</style>