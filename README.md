<div align="center">
<h1>Next NProgress bar</h1>

<p>NProgress integration on Next.js compatible with /app and /pages folders</p>
</div>

## Table of Contents

- [Getting started](#getting-started)
  - [Install](#install)
  - [Import](#import)
  - [Use](#use)
- [Exemple with /pages/\_app](#exemple-with-pagesapp)
  - [JavaScript](#javascript)
  - [TypeScript](#typescript)
- [Exemple with /app/layout](#exemple-with-applayout)
  - [JavaScript](#javascript)
    - [First approach in a use client layout](#first-approach-in-a-use-client-layout)
    - [Second approach wrap in a use client Providers component](#second-approach-wrap-in-a-use-client-providers-component)
  - [TypeScript](#typescript)
    - [First approach in a use client layout](#first-approach-in-a-use-client-layout)
    - [Second approach wrap in a use client Providers component](#second-approach-wrap-in-a-use-client-providers-component)
- [Props](#other-solutions)
  - [height](#height)
  - [color](#color)
  - [options](#options)
  - [appDirectory](#appdirectory)
  - [shallowRouting](#shallowrouting)
  - [delay](#delay)
  - [style](#style)
- [Issues](#issues)
- [LICENSE](#license)

## Getting started

### Install

```bash
npm install next-nprogress-bar
```

or

```bash
yarn add next-nprogress-bar
```

### Import

_Import it into your **/pages/\_app(.js/.jsx/.ts/.tsx)** or **/app/layout(.js/.jsx/.ts/.tsx)** folder_

```javascript
import ProgressBar from 'next-nprogress-bar';
```

### Use

```javascript
<ProgressBar />
```

## Exemple with /pages/\_app

### JavaScript

```jsx
import ProgressBar from 'next-nprogress-bar';

export default function App({ Component, pageProps }) {
  return (
    <>
      <Component {...pageProps} />
      <ProgressBar
        height="4px"
        color="#fffd00"
        options={{ showSpinner: false }}
        shallowRouting
      />
    </>
  );
}
```

### TypeScript

```tsx
import type { AppProps } from 'next/app';
import ProgressBar from 'next-nprogress-bar';

export default function App({ Component, pageProps }: AppProps) {
  return (
    <>
      <Component {...pageProps} />
      <ProgressBar
        height="4px"
        color="#fffd00"
        options={{ showSpinner: false }}
        shallowRouting
      />
    </>
  );
}
```

## Exemple with /app/layout

### JavaScript

#### First approach in a use client layout

```jsx
// In /app/layout.jsx
'use client';

import ProgressBar from 'next-nprogress-bar';

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        {children}
        <ProgressBar
          height="4px"
          color="#fffd00"
          options={{ showSpinner: false }}
          shallowRouting
          appDirectory
        />
      </body>
    </html>
  );
}
```

#### Second approach wrap in a use client Providers component

See [Next.js documentation](https://nextjs.org/docs/getting-started/react-essentials#rendering-third-party-context-providers-in-server-components)

```jsx
// Create a Providers component to wrap your application with all the components requiring 'use client', such as next-nprogress-bar or your different contexts...
'use client';

import ProgressBar from 'next-nprogress-bar';

const Providers = ({ children }) => {
  return (
    <>
      {children}
      <ProgressBar
        height="4px"
        color="#fffd00"
        options={{ showSpinner: false }}
        shallowRouting
        appDirectory
      />
    </>
  );
};

export default Providers;

// Import and use it in /app/layout.jsx
import Providers from './providers';

export const metadata = {
  title: 'Create Next App',
  description: 'Generated by create next app',
};

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <Providers>{children}</Providers>
      </body>
    </html>
  );
}
```

### TypeScript

#### First approach in a use client layout

```tsx
// In /app/layout.tsx
'use client';

import ProgressBar from 'next-nprogress-bar';

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>
        {children}
        <ProgressBar
          height="4px"
          color="#fffd00"
          options={{ showSpinner: false }}
          shallowRouting
          appDirectory
        />
      </body>
    </html>
  );
}
```

#### Second approach wrap in a use client Providers component

See [Next.js documentation](https://nextjs.org/docs/getting-started/react-essentials#rendering-third-party-context-providers-in-server-components)

```tsx
// Create a Providers component to wrap your application with all the components requiring 'use client', such as next-nprogress-bar or your different contexts...
'use client';

import ProgressBar from 'next-nprogress-bar';

const Providers = ({ children }: { children: React.ReactNode }) => {
  return (
    <>
      {children}
      <ProgressBar
        height="4px"
        color="#fffd00"
        options={{ showSpinner: false }}
        shallowRouting
        appDirectory
      />
    </>
  );
};

export default Providers;

// Import and use it in /app/layout.tsx
import Providers from './providers';

export const metadata = {
  title: 'Create Next App',
  description: 'Generated by create next app',
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>
        <Providers>{children}</Providers>
      </body>
    </html>
  );
}
```

## Props

### height _optional_ - _string_

Height of the progress bar - **by default 2px**

### color _optional_ - _string_

Color of the progress bar - **by default #0A2FFF**

### options _optional_ - _NProgressOptions_

**by default undefined**

See [NProgress docs](https://www.npmjs.com/package/nprogress#configuration)

### appDirectory _optional_ - _boolean_

If your are in the new **/app** directory - **by default false**

### shallowRouting _optional_ - _boolean_

If the progress bar is not displayed when you use shallow routing - **by default false**

See [Next.js docs](https://nextjs.org/docs/pages/building-your-application/routing/linking-and-navigating#shallow-routing)

### delay _optional_ - _number_

When the page loads faster than the progress bar, it does not display - **by default 0**

### style _optional_ - _string_

Your custom CSS - **by default [NProgress CSS](https://github.com/rstacruz/nprogress/blob/master/nprogress.css)**

## Issues

Please file an issue for bugs, missing documentation, or unexpected behavior.

[File an issue](https://github.com/Skyleen77/next-nprogress-bar/issues)

## LICENSE

MIT
