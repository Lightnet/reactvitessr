# react vite ssr

# LICENSE: MIT

# Create by: Lightnet

# Information:

  Manage to get some code working to run react with vite.

  Due to react-router-dom v6 update.

- https://vitejs.dev/guide/ssr
- https://github.com/vitejs/vite/tree/main/packages/playground/ssr-react

  It is base on the ssr github above the link.

react-router-dom v5
```js
import { StaticRouter } from "react-router-dom";
//...
export function render(url, context) {
  return ReactDOMServer.renderToString(
    <StaticRouter location={url} context={context}>
      <App />
    </StaticRouter>
  )
}
```

react-router-dom v6
```js
import { StaticRouter } from 'react-router-dom/server'
//...
export function render(url) {
  return ReactDOMServer.renderToString(
    <StaticRouter location={url}>
      <App />
    </StaticRouter>
  )
}
```
  Needed for the prerender script to build the html files.


react-router-dom v5 Switch 
```js
//...
const routes = Object.keys(pages).map((path) => {
  const name = path.match(/\.\/pages\/(.*)\.jsx$/)[1]
  return {
    name,
    path: name === 'Home' ? '/' : `/${name.toLowerCase()}`,
    component: pages[path].default
  }
})
//...
export function App() {
  return (
    <>
      <nav>
        <ul>
          {routes.map(({ name, path }) => {
            return (
              <li key={path}>
                <Link to={path}>{name}</Link>
              </li>
            )
          })}
        </ul>
      </nav>
      <Switch>
        {routes.map(({ path, component: RouteComp }) => {
          return (
            <Route key={path} path={path}>
              <RouteComp />
            </Route>
          )
        })}
      </Switch>
    </>
  )
}
```

react-router-dom v6 Routes 
```js
//...
const pageroutes = Object.keys(pages).map((path) => {
  const name = path.match(/\.\/pages\/(.*)\.jsx$/)[1]
  return {
    name,
    path: name === 'Home' ? '/' : `/${name.toLowerCase()}`,
    component: pages[path].default
  }
})
//...
export function App() {
  return (
    <>
      <nav>
        <ul>
          {pageroutes.map(({ name, path }) => {
            return (
              <li key={path}>
                <Link to={path}>{name}</Link>
              </li>
            )
          })}
        </ul>
      </nav>
      <Routes>
        {pageroutes.map(({ path, component: RouteComp }) => {
          return (
            <Route key={path} path={path} element={<RouteComp />  } />
          )
        })}
      </Routes>
    </>
  )
}
```
  Due to same name for routes had to add routes to pageroutes.


# set up:
- install the nodejs

## project dir:
- install the packages
```
$ npm install

```

To build the dev server.
```
$ npm run build
$ npm run generate
```

After building the files.
```
$ npm run dev
```
This will run the server and hot reload react.

# Notes:
- It took some time to read the code file to understand how it works.

# Links:
- https://reactrouter.com/docs/en/v6/guides/ssr