<script>
  import {FirebaseApp, User, Doc, Collection} from "sveltefire";

  import firebase from "firebase/app";
  import "firebase/firestore";
  import "firebase/auth";
  import "firebase/performance";
  import "firebase/analytics";
  import "firebase/storage";
  import ConnectedUser from "./User/ConnectedUser.svelte";
  import NotConnectedUser from "./User/NotConnectedUser.svelte";
  import Reward from "./Reward/Reward.svelte";

  let firebaseConfig = {
    apiKey: "AIzaSyDI7L78oCoXw9U_BiAXbfVbwSFgqGwCNiA",
    authDomain: "sibyla-ddabf.firebaseapp.com",
    databaseURL: "https://sibyla-ddabf.firebaseio.com",
    projectId: "sibyla-ddabf",
    storageBucket: "sibyla-ddabf.appspot.com",
    messagingSenderId: "893776553943",
    appId: "1:893776553943:web:332f7273f6ff650f760d92"
  };

  firebase.initializeApp(firebaseConfig);
</script>

<main>

  <FirebaseApp {firebase}>

    <h1>Sibylla Reward</h1>

    <User let:user let:auth>

      <div slot="signed-out">
        <NotConnectedUser {auth}/>
      </div>
      <ConnectedUser {user} {auth}/>

      <div class="reward-list">
        <Doc path={`users/${user.uid}`} let:data={userInfo} let:ref={userRef} log>
          <Collection path={userRef.collection('rewards')} let:data={rewards}>
            {#each rewards as reward}
              <Doc path={reward.reward} let:data={rewardInfo}>
                <Reward reward={rewardInfo}/>
              </Doc>
            {/each}
          </Collection>
        </Doc>

      </div>

    </User>
  </FirebaseApp>

</main>

<style>

  h1, em {
    color: #ff3e00;
  }

  div.reward-list{
    margin-top: 10px;
    display: flex;
  }
</style>