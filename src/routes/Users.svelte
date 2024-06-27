<script context="module">
    // Importing the createClient function from the Supabase JavaScript library
    import { createClient } from '@supabase/supabase-js';
  
    // Define Supabase client URL and anonymous (public) Key
    const SUPABASE_URL = 'https://psmylknncfknwdrbdfbe.supabase.co';
    const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InBzbXlsa25uY2ZrbndkcmJkZmJlIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MTU1MjE3MjksImV4cCI6MjAzMTA5NzcyOX0.la5rLXr36rgWzipajfBZ58Xd9dojLG50ED46M4vQhK0';
    // Set up a client connection (supabase) to interact with a Supabase project using a specific URL and anonymous key for authentication.
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>
  
  <script lang="ts">
    // Importing the onMount function from the Svelte framework
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
        // Try to fetch data from Supabase table 'users'
        const { data, error } = await supabase
          .from('users') // table name
          .select('login, first_name, last_name'); // column name(s)
        
        // If await returned an error object instead of data, display the message property for the error.
        if (error) {
          throw new Error(`Error fetching data: ${error.message}`);
        }
  
        // Ensure users is an array, even if data is null or undefined to prevent potential errors when accessing 'users.length' or iterating through 'users'.
        users = data ?? []; // Explanation of ??: In JavaScript and TypeScript, the ?? operator is called the "nullish coalescing operator." It provides a way to handle default values when dealing with 'null' or 'undefined' values. 
        
      // Handle any exception (error) thrown anywhere within the try block gracefully.
      } catch (error) {
        // Display any exception (error) message(s) to the browser console.
        console.error(error);
      }
    });
  </script>
  
  <h1>All Users</h1>
    
 <!-- Render table of users if data is available (users.length > 0), otherwise displays a loading message (Fetching data...). --> 
  {#if users.length > 0}
    <table>
      <thead>
        <!-- Table Heading -->
        <tr>
          <th>Login</th>
          <th>First Name</th>
          <th>Last Name</th>
        </tr>
      </thead>
      <tbody>
        <!-- Iterate over each user and display its properties in each cell <td> inside each table row <tr> -->
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
  