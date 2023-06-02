<!-- FileComponent.svelte -->
<svelte:options tag="web-comp" />
<script>
  import { onMount } from 'svelte';

  let name = '';
  let type = 'File';
  let selectedFolder = '';
  let folders = {};
  let showFolders = []
  let keyobjAray = []

  const save = () => {
    if (type === 'File') {
      //save files
      if(name === ''){
        alert("error: input some file name")
      }
      else{
        if(selectedFolder){
          folders[selectedFolder].push(name)
          alert(`Saving file "${name}" in folder "${selectedFolder}"`);
      }
      else{
          folders.files.push(name)
          alert(`Saving file "${name}" in root folder`);
      }
      }
      console.log(folders);
    } else if (type === 'Folder') {
      // Save folder
      if(name === ''){
        alert("error: input some folder name")
      }
      else{
        folders={...folders,[name]:[]}
        alert(`Saving folder "${name}"`);
        console.log(folders);
      }
    } else {
      console.error('Invalid selection');
    }
    resetForm();
  };

  const resetForm = () => {
    name = '';
    type = 'File';
    selectedFolder = '';
     keyobjAray = Object.keys(folders)
     showFolders = keyobjAray.splice(1,keyobjAray.length)
  };

  const cancel = () => {
    resetForm();
  };

  onMount(() => {
    // Simulating fetching folders from an API
       folders = {"files":[],"folder1":[],"folder2":[]};
        keyobjAray = Object.keys(folders)
        console.log(keyobjAray);
     showFolders = keyobjAray.splice(1,keyobjAray.length)
  });
</script>

<h2 style="font-family: Times New Roman,Times">ADD Name</h2>
<input style= "padding:2%;font-family: Times New Roman,Times" type="text" placeholder="File Name or Folder Name" bind:value={name} />

<h2 style="font-family: Times New Roman,Times">Select Type</h2>
<select bind:value={type}>
  <option value="File">File</option>
  <option value="Folder">Folder</option>
</select>

{#if type === 'File'}
  <h2 style="font-family: Times New Roman,Times">Select Folder</h2>
  <select bind:value={selectedFolder}>
    <option value="">None</option>
    {#each showFolders as folder}
      <option value={folder}>{folder}</option>
    {/each}
  </select>
{/if}
<div style="margin-top: 2%; text-align: center;">
    <button style="color: green; margin-left: .5%;margin;" on:click={save}>Save</button>
    <button style="color: red;margin-left: .5%;" on:click={cancel}>Cancel</button>
</div>