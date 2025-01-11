# Svelte Flow Learning Project

Welcome to the Svelte Flow Learning Project! This project is designed to help you learn both Svelte and the Svelte Flow library. Below you will find an overview of the project, setup instructions, and resources to help you get started.

## Table of Contents

- [Introduction](#introduction)
- [Project Structure](#project-structure)
- [Setup Instructions](#setup-instructions)
- [Usage](#usage)
- [Resources](#resources)
- [Contributing](#contributing)
- [License](#license)

## Introduction

This project aims to provide a hands-on learning experience with Svelte and the Svelte Flow library. Svelte is a modern JavaScript framework for building user interfaces. Svelte Flow is a library for creating flow graphs in Svelte applications.

## Project Structure

The project structure is as follows:

```
svelte-flow/
├── .gitignore
├── .npmrc
├── .prettierignore
├── .prettierrc
├── LICENSE
├── package-lock.json
├── package.json
├── README.md
├── svelte.config.js
├── tsconfig.json
├── vite.config.ts
├── src/
│   ├── app.d.ts
│   ├── app.html
│   ├── lib/
│   │   ├── FlowComponent.svelte
│   │   └── index.ts
│   └── routes/
│       └── +page.svelte
└── static/
    └── favicon.png
```

# Project created using sv command

Everything you need to build a Svelte project, powered by [`sv`](https://github.com/sveltejs/cli).

### How was it created

If you're it was already done. Congrats!

```bash
# create a new project in the current directory
npx sv create

# create a new project in my-app
npx sv create my-app
```

### Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

### Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://svelte.dev/docs/kit/adapters) for your target environment.

## Setup Instructions

To get started with this project, follow these steps:

1. **Clone the repository:**

    ```bash
    git clone https://github.com/DominikKowalczyk/svelte-flow.git
    cd svelte-flow
    ```

2. **Install dependencies:**

    ```bash
    npm install
    ```

3. **Run the development server:**

    ```bash
    npm run dev
    ```

4. **Open your browser:**

    Navigate to `http://localhost:5000` to see the application in action.

## Usage

This project includes examples and exercises to help you learn Svelte and Svelte Flow. Explore the `src/components` and `src/stores` directories to see how components and state management are implemented.

## Resources

Here are some resources to help you learn more about Svelte and Svelte Flow:

- [Svelte Documentation](https://svelte.dev/docs)
- [Svelte Tutorial](https://svelte.dev/tutorial)
- [Svelte Flow GitHub Repository](https://github.com/xyflow/xyflow)

## Contributing

Contributions are welcome! If you have any suggestions or improvements, please create an issue or submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

Happy coding!


