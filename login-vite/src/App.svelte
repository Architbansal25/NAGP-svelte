<!-- Login.svelte -->
<script>
  let username = '';
  let password = '';

  function handleLogin() {
    // login check
    if (username === 'admin' && password === '123') {
      window.location.href = 'https://tubular-treacle-7e3694.netlify.app/';
    } else {
      alert('Invalid username or password');
    }
    resetForm();
  }
 const resetForm =()=>{
    username = '',
    password = ''
  }
</script>

<div style="text-align: center;">
  <h2 style="font-family: Times New Roman,Times">Svelte learning</h2>
<div>

    <label style="font-family: Times New Roman,Times" for="username">Username</label>
    <input style="font-family: Times New Roman,Times" type="text" id="username" bind:value={username} />
    
    <div style="margin-left: .5%; margin-top: 2%">
      <label style="font-family: Times New Roman,Times" for="password">Password</label>
      <input style="font-family: Times New Roman,Times;" type="password" id="password" bind:value={password} />
    </div>
</div>

<button style="font-family: Times New Roman,Times; color: green; margin-top: 1.5%;"on:click={handleLogin}>Login</button>
</div>
