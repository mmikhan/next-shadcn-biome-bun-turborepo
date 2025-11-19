# Next.js ShadCN Biome Bun Turborepo

> ShadCN Compiled Package Setup with project specific Biome configuration using Ultracite

It's a result of my recent interest of learning Turborepo + Monorepo setup. While setting up everything, I realized the default ShadCN monorepo is a Just-In-Time package setup whereas, Turborepo itself [recommends](https://turborepo.com/docs/core-concepts/internal-packages#compiled-packages) a Compiled package setup. Both approaches have their pros and cons. There's nothing wrong or right with either of them. It depends on the project's requirements and preferences.

## Just-In-Time vs Compiled Packages

- When using Just-In-Time internal UI package, Turbo can still cache the consuming app built but that's most likely going to change a lot since this is where you are going to work and make changes. Since Turbo couldn't cache the internal UI built output, built time is going up a little every time building the consuming app.
- When using the Compiled package building the internal UI package using it's own build script, Turbo can cache the built output. i.e.: `/dist`.
- When using the compiled internal UI package, that means we are also duplicating the CSS classes from the internal package itself and as well as the consuming app. One way we could avoid this is by not building the styles from the internal UI package but use the `@source` directive inside the stylesheet from Tailwind CSS from the consuming app so only one set of styles are being generated from the consumed level. ShadCN UI's default monorepo does the opposite. It scans the CSS selectors from outside of the internal UI package. That also works but again, we miss the Turbo build cache for the internal UI package CSS output.

### Apps and Packages

- `web`: another [Next.js](https://nextjs.org/) app with [Tailwind CSS](https://tailwindcss.com/)
- `ui`: a stub React component library with [Tailwind CSS](https://tailwindcss.com/) shared by both `web` and `docs` applications
- `@repo/shadcn`: `shadcn` compiled package configurations
- `@repo/typescript-config`: `tsconfig.json`s used throughout the monorepo

Each package/app is 100% [TypeScript](https://www.typescriptlang.org/).
