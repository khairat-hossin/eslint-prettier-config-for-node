For a Node.js developer, using ESLint and Prettier together helps maintain consistent code style and catch potential issues. Here's a recommended configuration:

### Step 1: Install Required Packages

Run the following commands to install ESLint, Prettier, and the necessary plugins:

```bash
npm install --save-dev eslint prettier eslint-config-prettier eslint-plugin-prettier eslint-plugin-node
```

- `eslint`: Lints JavaScript code.
- `prettier`: Formats code.
- `eslint-config-prettier`: Disables ESLint rules that conflict with Prettier.
- `eslint-plugin-prettier`: Runs Prettier as an ESLint rule.
- `eslint-plugin-node`: Provides rules specific to Node.js.

### Step 2: Configure ESLint

Create a `.eslintrc.json` file in your project root and add the following configuration:

```json
{
  "env": {
    "node": true,
    "es2021": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:node/recommended",
    "plugin:prettier/recommended"
  ],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error",
    "no-console": "off",
    "node/no-unsupported-features/es-syntax": [
      "error",
      { "ignores": ["modules"] }
    ]
  },
  "parserOptions": {
    "ecmaVersion": 12,
    "sourceType": "module"
  }
}
```

### Step 3: Configure Prettier

Create a `.prettierrc` file for Prettier settings:

```json
{
  "semi": true,
  "singleQuote": true,
  "trailingComma": "all",
  "printWidth": 80,
  "tabWidth": 2
}
```

### Step 4: Add ESLint and Prettier Scripts

In your `package.json`, add these scripts to lint and format your code easily:

```json
"scripts": {
  "lint": "eslint .",
  "format": "prettier --write ."
}
```

### Step 5: Optional VSCode Configuration

To enable auto-formatting on save in VSCode, add the following to your `.vscode/settings.json`:

```json
{
  // Enable format on save
  "editor.formatOnSave": true,

  // Set Prettier as the default formatter
  "editor.defaultFormatter": "esbenp.prettier-vscode",

  // Enable ESLint auto-fix on save
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true // This will apply ESLint fixes on save
  },

  // Validate ESLint for these file types
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ]
}
```

With this setup, ESLint will handle code linting, while Prettier ensures code formatting, and the two won't conflict.
