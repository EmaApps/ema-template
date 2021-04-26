# Working with routes

Ema gives you the freedom to use any Haskell type for representing your site routes. You don't need complicated rewrite rules. Routes are best represented using what are known as *sum  types* (or ADT, short for *Abstract Data Type*). Here's an example of a route type:

```haskell
data Route 
  = Index
  | About
```

This type represents two routes pointing to -- the index page (`/`) and the about page (`/about`). Designing the route type is only half the job; you will also need to tell Ema how to convert it to / from the browser URL. This is achieved by writing an instance for the `Ema` typeclass:

```haskell
class Ema MyModel Route where 
  -- Convert our route to browser URL, represented as a list of slugs
  encodeRoute = \case
    Index -> []  -- An empty slug represents the index route: index.html
    About -> ["about"]
  -- Convert back the browser URL, represented as a list of slugs, to our route
  decodeRoute = \case
    [] -> Just Index
    ["about"] -> Just About
    _ -> Nothing
  -- The third method is used during static site generation. 
  -- This tells Ema which routes to generate .html files for.
  staticRoutes model =
    [Index, About]
  -- The fourth method is optional; if you have static assets to serve, specify
  -- them here. Paths are relative to current working directory.
  staticAssets Proxy =
    ["css", "images", "favicon.ico", "resume.pdf"]
  ```

(The `MyModel` type is explained in the [earlier section](guide/model.md)).

That is all there is to it. 

You can use whatever complex route types to model your website's routes, as long as those types are isomorphic to the [slug](concepts/slug.md) list. 

## Advanced example

Here's one possible way to design the route type for a weblog site,

```haskell
data Route
  = Home 
  | Blog BlogRoute
  | Tag TagRoute

data BlogRoute
  = BlogIndex
  | BlogPost Ema.Slug

data TagRoute
  = TagListing
  | Tag Tag

newtype Tag = Tag Text
```

Defining *hierarchical routes* like this is useful if you want to render *parts* of your HTML as being common to only a subset of your site, such as adding a blog header to all blog pages, but not to tag pages.

{.last}
[Next]{.next}, with our model and routes in place, [we will define the HTML for our site](guide/render.md) using Ema.