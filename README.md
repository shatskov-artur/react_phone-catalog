# Phone Catalog

An e-commerce product catalog built with React 19, TypeScript and Redux Toolkit — browsing,
filtering, a cart and a favourites list, with state that survives a page reload.

**[▶ Open it](https://shatskov-artur.github.io/react_phone-catalog)**

## What it does

Six routes covering the shopping flow end to end:

| Route | Purpose |
|---|---|
| Home | featured products, category entry points |
| Catalog | phones / tablets / accessories with sorting and pagination |
| Product details | gallery, colour and capacity selection, specs, suggestions |
| Cart | quantity control, running total |
| Favourites | saved items |
| 404 | not-found fallback |

## How it is built

```
src/modules/pages/       one folder per route
src/modules/components/  reusable UI — Breadcrumbs, Dropdown, CartItem,
                         ColorSelector, CapacitySelector, BurgerMenu, EmptyState …
src/store/               Redux Toolkit — cartSlice, favouritesSlice
src/api/                 data fetching
src/types/               shared TypeScript types
```

~1,850 lines of TypeScript across roughly 30 components.

**State.** Cart and favourites are Redux Toolkit slices rather than component state, because both
are read and mutated from places that are nowhere near each other in the tree — a product card in
the catalog, the details page, the header counter, the cart itself. Prop-drilling that would mean
threading handlers through every layer; a slice means each of those places talks to the store
directly. Both slices persist to `localStorage`, so a reload doesn't empty the cart.

**Components.** Every component is a folder with its implementation, its stylesheet and an
`index.ts` barrel, so an import is `components/Dropdown` rather than a path into the file tree.
Selection widgets (colour, capacity) are separate components because the same control appears in
more than one place with different data.

**Typing.** Product shapes live in `src/types` and are shared between the API layer, the store and
the components, so a change to the product model surfaces at compile time in every place that
reads it instead of at runtime in one of them.

## Running locally

```bash
npm install
npm run dev      # dev server
npm run build    # production build
npm run lint     # eslint
npm run preview  # serve the build
```

## Stack

React 19, TypeScript, Redux Toolkit, React Router 7, Vite, SCSS, Cypress.

## Origin

Built as a Mate Academy course project. The product data set and the design specification came
from the course; the application — routing, state layer, components and styling — is mine.
