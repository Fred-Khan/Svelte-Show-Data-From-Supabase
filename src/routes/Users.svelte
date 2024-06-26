<script context="module">
    import { createClient } from '@supabase/supabase-js';
  
    // Initialize Supabase client
    const SUPABASE_URL = 'https://psmylknncfknwdrbdfbe.supabase.co';
    const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InBzbXlsa25uY2ZrbndkcmJkZmJlIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MTU1MjE3MjksImV4cCI6MjAzMTA5NzcyOX0.la5rLXr36rgWzipajfBZ58Xd9dojLG50ED46M4vQhK0';
    
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>
  
  <script lang="ts">
    import { onMount } from 'svelte';
  
    // Type declaration for each user object
    type User = {
      login: string;
      first_name: string;
      last_name: string;
    };
  
    // Initialize users as an array of User objects
    export let users: User[] = [];
  
    onMount(async () => {
      try {
        // Fetch data from Supabase table 'users'
        const { data, error } = await supabase
          .from('users')
          .select('login, first_name, last_name');
  
        if (error) {
          throw new Error(`Error fetching data: ${error.message}`);
        }
  
        users = data ?? []; // Ensure users is an array, even if data is null or undefined
      } catch (error) {
        console.error(error);
      }
    });
  </script>
  
  <h1>All Users</h1>
    
  {#if users.length > 0}
    <table>
      <thead>
        <tr>
          <th>Login</th>
          <th>First Name</th>
          <th>Last Name</th>
        </tr>
      </thead>
      <tbody>
        {#each users as user}
          <tr>
            <td>{user.login}</td>
            <td>{user.first_name}</td>
            <td>{user.last_name}</td>
          </tr>
        {/each}
      </tbody>
    </table>
  {:else}
    <p>Fetching data...</p>
  {/if}
  