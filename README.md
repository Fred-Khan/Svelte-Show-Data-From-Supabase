# Svelte Supabase Data Fetching Example

This project demonstrates how to fetch data from a Supabase database table and display it using Svelte. It utilises Supabase's API to retrieve user data and presents it in an HTML table using Svelte components.

## Files Explained

### `src/routes/+page.svelte`

This file serves as the main entry point for a Svelte page. It imports the `AllUsers` component to display all fetched user data.

- **Purpose:** 
  - Provides an entry point for rendering the `AllUsers` component.
  - Displays links to documentation for Supabase and Svelte.

### `src/routes/Users.svelte`

This file contains the main logic for fetching and displaying user data from Supabase.

- **Context Module Script:**
  - Initializes the Supabase client using credentials (`SUPABASE_URL` and `SUPABASE_ANON_KEY`).
  - **Purpose:** 
    - Sets up the Supabase client to interact with the Supabase service.
  
- **Main Script:**
  - Imports necessary Svelte functions (`onMount`) and defines the `User` type.
  - Initializes an empty array `users` to store fetched user data.
  - Uses `onMount` to asynchronously fetch data from the `users` table using Supabase's `select` method.
  - **Purpose:**
    - Fetches data from the Supabase `users` table and handles errors.
    - Populates the `users` array with retrieved data.

- **Template:**
  - Conditionally renders content based on whether data is being fetched (`users.length > 0`).
  - Displays a table with user data (`user.login`, `user.first_name`, `user.last_name`) if data is available.
  - Shows a "Fetching data..." message if data is still loading.
  - **Purpose:**
    - Renders the fetched user data in an HTML table structure.

## Usage

1. Clone the repository.
2. Install dependencies using `npm install`.
3. Run the project using `npm run dev`.

## Creating Your Own
### Supabase
1. Create a table called users in Supabase
2. Create the following fields as text:
   - login
   - first_name
   - last_name
3. Add at least one row of data.
4. Create Row Level Security Policy (Authentication => Policies)
   - Use *SELECT	Enable read access for all users*	template
   - Save Policy

### Svelte
1. Create a new Svelte Skeleton TypeScript project:
```bash
npm create svelte@latest Svelte-Show-Data-From-Supabase
cd Svelte-Show-Data-From-Supabase
npm install
```
2. Install the Supabase client library:
```bash
npm install @supabase/supabase-js
```
3. Start coding!

## Additional Resources

- [Svelte Documentation](https://kit.svelte.dev): Learn more about Svelte.
- [Supabase Documentation](https://supabase.com/docs#reference-documentation): Explore Supabase's API and functionality.

