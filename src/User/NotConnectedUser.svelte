<script>
   export let auth

   let email = 'gregoire.lecun@gmail.com';
   let password = 'gregoire';

   function signIn() {
      auth.signInWithEmailAndPassword(email, password).catch(function(error) {
         let errorCode = error.code;
         let errorMessage = error.message;
         if (errorCode === 'auth/wrong-password') {
            alert('Mot de passe incorrect');
         } else if (errorCode === 'auth/user-not-found') {
            alert('Aucun utilisateur correspondant au mail');
         } else {
            alert(errorMessage);
         }
      });
   }
</script>

<main>
   <input placeholder="Email" bind:value={email}>
   <input placeholder="Mot de passe" type="password" bind:value={password}>
   <button on:click={() => signIn()}>
      Connexion
   </button>
</main>