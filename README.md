
## 👉 Get Started
Install dependencies
```
npm install
```
Update your `.env` file with values for each environment variable
```
API_KEY=AIzaSyBkkFF0XhNZeWuDmOfEhsgdfX1VBG7WTas
etc ...
```
Run your local database

_Note: Local database is powered by [json-server](https://github.com/typicode/json-server) and writes to `db.json`. It's just for prototyping. You'll need to update `api/_db.js` and connect to your database of choice before deployment._
```
npm run json-server
```
Run the development server
```
npm run start
```
In a separate terminal window run your API endpoints 
```
node api
```
When the above command completes you'll be able to view your website at `http://localhost:3000`

## 🥞 Stack
This project uses the following libraries and services:
- Framework - [Create React App](https://create-react-app.dev) with React Router
- UI Kit - [Bootstrap](https://react-bootstrap.github.io)
- Authentication - [Firebase Auth](https://firebase.google.com/products/auth)
- Database - TBD
- Payments - [Stripe](https://stripe.com)
- Contact Form - [Google Sheets](https://www.google.com/sheets/about/)
- Analytics - [Google Analytics](https://googleanalytics.com)
- Hosting - TBD


## 📚 Guide

<details> <summary><b>Styles</b></summary> <p> You can edit Bootstrap SASS variables in the global stylesheet located at <code><a href="src/styles/global.scss">src/styles/global.scss</a></code>. Variables allow you to control global styles (like colors and fonts), as well as element specific styles (like button padding). Before overriding Bootstrap elements with custom style check the <a href="https://getbootstrap.com/docs/4.3/getting-started/introduction/">Bootstrap docs</a> to see if you can do what need by tweaking a SASS variable. </p> <p> Custom styles are located in their related component's directory. For example, if any custom style is applied to the <code>Navbar</code> component you'll find it in <code>src/components/Navbar.scss</code>. We ensure custom styles are scoped to their component by prepending the classname with the component name (such as <code>.Navbar__brand</code>). This ensures styles never affect elements in other components. If styles need to be re-used in multiple components consider creating a new component that encapsulates that style and structure and using that component in multiple places. </p> </details>

<details>
<summary><b>Routing</b></summary>
<p>
  This project uses <a target="_blank" href="https://reacttraining.com/react-router/web/guides/quick-start">React Router</a> and includes a convenient <code>useRouter</code> hook (located in <code><a href="src/util/router.js">src/util/router.js</a></code>) that wraps React Router and gives all the route methods and data you need.

```js
import { Link, useRouter } from "./../util/router.js";

function MyComponent() {
  // Get the router object
  const router = useRouter();

  // Get value from query string (?postId=123) or route param (/:postId)
  console.log(router.query.postId);

  // Get current pathname
  console.log(router.pathname);

  // Navigate with the <Link> component or with router.push()
  return (
    <div>
      <Link to="/about">About</Link>
      <button onClick={(e) => router.push("/about")}>About</button>
    </div>
  );
}
```
</p>
</details>

<details>
<summary><b>Authentication</b></summary>
<p>
  This project uses <a href="https://firebase.google.com">Firebase Auth</a> and includes a convenient <code>useAuth</code> hook (located in <code><a href="src/util/auth.js">src/util/auth.js</a></code>) that wraps Firebase and gives you common authentication methods. Depending on your needs you may want to edit this file and expose more Firebase functionality.

```js
import { useAuth } from "./../util/auth.js";

function MyComponent() {
  // Get the auth object in any component
  const auth = useAuth();

  // Depending on auth state show signin or signout button
  // auth.user will either be an object, null when loading, or false if signed out
  return (
    <div>
      {auth.user ? (
        <button onClick={(e) => auth.signout()}>Signout</button>
      ) : (
        <button onClick={(e) => auth.signin("hello@divjoy.com", "yolo")}>Signin</button>
      )}
    </div>
  );
}
```
</p>
</details>

<details>
<summary><b>Database</b></summary>
<p>
  This project wasn't setup with a particular database in mind, but includes some data fetching hooks to get you started (located in <code><a href="src/util/db.js">src/util/db.js</a></code>) and a basic REST API (located in <code><a href="api">api</a></code>) where you can connect to your database of choice.
      

```js
import { useAuth } from './../util/auth.js';
import { useItemsByOwner } from './../util/db.js';
import ItemsList from './ItemsList.js';

function ItemsPage(){
  const auth = useAuth();

  // Fetch items by owner
  // Returned status value will be "idle" if we're waiting on
  // the uid value or "loading" if the query is executing.
  const uid = auth.user ? auth.user.uid : undefined;
  const { data: items, status } = useItemsByOwner(uid);

  // Once we have items data render ItemsList component
  return (
    <div>
      {(status === "idle" || status === "loading") ? (
        <span>One moment please</span>
      ) : (
        <ItemsList data={items}>
      )}
    </div>
  );
}
```
</p>
</details>

<details>
<summary><b>Deployment</b></summary>
<p>
Build your front-end for deployment

```
npm run build
```

Then upload or deploy to your host. Exact details depend on your chosen host.

Your host may automatically read your environment variables from your `.env` file. If not, be sure to add each variable from `.env` to your host through their own UI. You can skip the ones in the lower section of `.env` (prepended with "REACT_APP\_") because those were already bundled into your front-end when you ran `npm run build`.

Have your host run `node api` to serve your web app. This will run a Node server that handles both your API endpoints and front-end. By default your server will be listening on port `8080`, but if your host expects a different port then you can set that by specifying a `PORT` environment variable. Some hosts will automatically set this environment variable to their desired port.

You can find extended information and host-specific details in the Create React App <a href="https://create-react-app.dev/docs/deployment">deployment docs</a>.
</p>
</details>

<details>
<summary><b>Other</b></summary>
<p>
  This project was created using <a href="https://divjoy.com?ref=readme_other">Divjoy</a>, the React codebase generator. You can find more info in the <a href="https://docs.divjoy.com">Divjoy Docs</a>.
</p>
</details>
  