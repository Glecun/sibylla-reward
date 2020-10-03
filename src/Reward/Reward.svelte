<script>
   import {StorageRef} from "sveltefire";
   import { fly } from 'svelte/transition';
   import firebase from "firebase/app";

   export let reward
   let upload = firebase.storage().ref();
</script>

{#await upload.child(reward.imageName).getDownloadURL()}
{:then url}
   <main in:fly={{x:50}}>
      <img alt={reward.imageName} src={url} />
      {reward.description}
   </main>
{/await}

<style>
   main {
      display: flex;
      flex-direction: column;
      align-items: center;
      border: 1px solid black;
      width: 200px;
      height: 250px;
      box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
      margin-right: 14px;
   }

   main img {
      width: 200px;
      height: 200px;
   }

</style>