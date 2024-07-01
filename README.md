# `svelte-ast-print`

![NPM Version](https://img.shields.io/npm/v/svelte-ast-print?style=for-the-badge&logo=npm)

Print **Svelte AST** nodes as a string.\
A.k.a. [`parse`] in reverse.\

This is what you need to create [codemods] - e.g. for migration between Svelte versions syntaxes.

## Documentation

<https://xeho91.github.io/svelte-ast-print>

## Acknowledgements

This package depends on:

- [`esrap`] for printing [ESTree] specification-compliant AST nodes

## Limitations

1. It doesn't print formatted output.\
   The primary goal is to be able to write codemods as soon as possible - because right now, there are no alternatives.

   If you need to format modified Svelte AST, use available formatters for Svelte:

   - [Biome](https://github.com/biomejs/biome) - _⚠️ has partial support_
   - [Prettier](https://github.com/prettier/prettier) with [`prettier-plugin-svelte`](https://github.com/sveltejs/prettier-plugin-svelte)

2. Is not optimized for performance yet - See [Roadmap](https://github.com/xeho91/svelte-ast-print/discussions/2)

## Getting started

1. Use the package manager of your choice to install this package:

   <details>
       <summary>npm</summary>

   ```sh
   npm install svelte-ast-print
   ```

   </details>

   <details>
       <summary>yarn</summary>

   ```sh
   yarn add svelte-ast-print
   ```

   </details>

   <details>
       <summary>pnpm</summary>

   ```sh
   pnpm add svelte-ast-print
   ```

   </details>

   <details>
       <summary>bun</summary>

   ```sh
   bun add svelte-ast-print
   ```

   </details>

1. Incorporate it into your project, for example with the Svelte [`parse`] method:

   ```ts
   import fs from "node:fs";

   import { print } from "svelte-ast-print";
   import { parse } from "svelte/compiler";


   const originalSvelteCode = fs.readFileSync("src/App.svelte", "utf-8");

   let svelteAST = parse(originalSvelteCode, { modern: true });

   // ...
   // Do some modifications on this AST...
   // e.g. transform `<slot />` to `{@render children()}`
   // ...

   const svelteCode = print(svelteAST); // AST goes back to string! 🎉

   fs.writeFileSync("src/App.svelte", svelteCode, { encoding: " utf-8" });
   ```

## Contributing

Take a look at [contributing guide](./.github/CONTRIBUTING.md).

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification.
**Contributions of any kind are welcome!**

💌 to these people:

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/xeho91"><img src="https://avatars.githubusercontent.com/u/18627568?v=4?s=100" width="100px;" alt="Mateusz Kadlubowski"/><br /><sub><b>Mateusz Kadlubowski</b></sub></a><br /><a href="https://github.com/xeho91/svelte-ast-print/commits?author=xeho91" title="Code">💻</a> <a href="#maintenance-xeho91" title="Maintenance">🚧</a> <a href="https://github.com/xeho91/svelte-ast-print/commits?author=xeho91" title="Documentation">📖</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

## Support

If you don't have time, but you need this project to work, or resolve an existing issue, consider sponsorship.

## Author

Mateusz "[xeho91](https://github.com/xeho91)" Kadlubowski

## License

![Project License](https://img.shields.io/github/license/xeho91/svelte-ast-print?style=for-the-badge)

This project is licensed under the [MIT License](./LICENSE.md).

<!-- links -->
[`esrap`]: https://github.com/rich-harris/esrap
[ESTree]: https://github.com/estree/estree
[codemods]: https://codemod.com/blog/what-are-codemods#ill-find-replace-whats-the-issue-hint-a-lot
[`parse`]: https://svelte.dev/docs/svelte-compiler#parse