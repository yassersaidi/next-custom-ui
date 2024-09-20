# Project Setup and Configuration
## Follow these steps to properly configure your Next.js project after installation via `create-next-app.`

### 1. Clean Build Artifacts
Add the following script to your `package.json` for removing the `.next` directory:

```json
"clean": "rm -rf .next"
```
### 2. ESLint Configuration
Refer to the official ESLint plugin documentation for Next.js and apply any necessary configurations:
[Next.js ESLint Plugin Documentation](https://nextjs.org/docs/pages/building-your-application/configuring/eslint#eslint-plugin)

### 3. Run ESLint
To check your code quality, run the linting command:

```bash
npm run lint
```

### 4. Prettier for Code Formatting
Set up Prettier as a code formatter:
1- [Install the Prettier VS Code Extension: Prettier - Code Formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode).

2- Install Prettier as a dev dependency:
```bash
npm install --save-dev eslint-config-prettier
```

3- Add "prettier" to the extends array in your `.eslintrc.json`.

4- Create a `.prettierrc.json` file with the following configuration:
```json
{
  "semi": true,
  "singleQuote": false,
  "quoteProps": "as-needed",
  "bracketSpacing": true,
  "tabWidth": 2,
  "useTabs": true,
  "bracketSameLine": false,
  "arrowParens": "always",
  "trailingComma": "es5",
  "singleAttributePerLine": true
}
```
5- To sort imports, install the following plugin:
```bash
npm install --save-dev @trivago/prettier-plugin-sort-imports
```
Update .prettierrc.json with:
```json
"importOrder": [
  "^next(/.*)?$",
  "^react(/.*)?$",
  "<THIRD_PARTY_MODULES>",
  "^@",
  "^[./]"
],
"importOrderSeparation": true,
"importOrderSortSpecifiers": true,
"plugins": ["@trivago/prettier-plugin-sort-imports"]
```

For more Prettier options, refer to the official documentation:
[Prettier Options](https://prettier.io/docs/en/options).

### 5. ESLint Rules
Add custom linting rules to your `.eslintrc.json`. Example:

```json
"rules": {
  "prefer-arrow-callback": "error",
  "no-const-assign": "error",
  "prefer-template": "error",
  "semi": "error",
  "quotes": "error",
  "no-trailing-spaces": "error"
}
```
For additional rules, see the [ESLint rules documentation](https://eslint.org/docs/latest/rules/).

### 6.VS Code Auto-Fix on Save
Configure VS Code to automatically fix errors on file save:

Create a `.vscode/settings.json` file with the following content:
```json
{
  "typescript.tsdk": "node_modules/typescript/lib",
  "files.autoSave": "onFocusChange",
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.addMissingImports.ts": true,
    "source.removeUnusedImports": true
  }
}
```

### 7. Tailwind CSS Class Sorting
Automatically sort Tailwind CSS classes with Prettier:

Install the required Prettier plugin:
```bash
npm install -D prettier prettier-plugin-tailwindcss
```
Add it to your `.prettierrc.json:`
```json
"plugins": [
  "@trivago/prettier-plugin-sort-imports",
  "prettier-plugin-tailwindcss"
]
```

### 8. Kebab-Case File Naming
Enforce kebab-case for file names:

Install the ESLint plugin:
```bash
npm install eslint-plugin-check-file --save-dev
```
Add the following configuration to your `.eslintrc.json:`
```json
"plugins": ["check-file"],
"rules": {
  "check-file/filename-naming-convention": [
    "error",
    { "**/*.{ts,tsx}": "KEBAB_CASE" },
    { "ignoreMiddleExtensions": true }
  ],
  "check-file/folder-naming-convention": [
    "error",
    { "**/!^[.]*": "KEBAB_CASE" }
  ]
}
```
### 9. Fix TailwindCSS @rule Errors
To resolve unknown Tailwind CSS at-rule errors in globals.css, update the `.vscode/settings.json` file:

```json
"files.associations": {
  "*.css": "tailwindcss"
}
```

### 10. Use Installed TypeScript Version
Ensure VS Code uses the installed TypeScript version for Next.js:

Open .vscode/settings.json and add:
```json
"typescript.tsdk": "node_modules/typescript/lib"
```

### 11. Typed Routes in Next.js
Enable typed routes for Next.js by adding the following to `next.config.mjs`:

```javascript
experimental: {
  typedRoutes: true
}
```
This helps catch route errors when using the Link component.

### 12. Custom Tab Labels in VS Code
Customize tab labels for better context in VS Code:

Add this to `.vscode/settings.json`:
```json
"workbench.editor.customLabels.patterns": {
  "**/app/**/page.tsx": "${dirname} - Page",
  "**/app/**/layout.tsx": "${dirname} - Layout",
  "**/components/**/index.tsx": "${dirname} - Component"
}
```

## Happy Coding :)
