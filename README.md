Language: [🇺🇸](./README.md) [🇯🇵](./README.ja.md)

[![Deploy](https://github.com/yKicchan/awesome-marp-template/actions/workflows/deploy.yml/badge.svg)](https://github.com/yKicchan/awesome-marp-template/actions/workflows/deploy.yml)

# Awesome Marp Template

This repository is a template repository that allows you to create slides utilizing [Marp](https://marp.app/) to its fullest potential, with ease.

## 🚀 Features

- 🚀 Automatic deployment to [GitHubPages](https://yKicchan.github.io/awesome-marp-template/) via [GitHubActions](./.github/workflows/deploy.yml)
- 🖼️ Support for setting OGP images for the title slide
- 🚄 Lightweight slide creation using Markdown extended syntax
- 🎨 Diverse slide expressions with CSS utility classes
- 🔧 A script to easily create new slides from the template

For demo slides using this repository, please refer to [GitHubPages](https://yKicchan.github.io/awesome-marp-template/demo).  
Build your own original slide environment using Markdown extended syntax and CSS utility classes!

## 📂 Directory Structure

The contents of the main directories and files are as follows.  
Feel free to customize them to suit your preferences!

```plaintext
.
├── .marprc.yml     # Marp CLI configuration file
├── engine.mjs      # Marp CLI engine extension
├── scripts/
│   ├── check       # Script to check if the OGP URLs for the slides are correct
│   ├── init        # Script for repository setup
|   └── new         # Script to create new slides from the template
├── src/            # Slide directory for deployment
│    └── demo/      # Demo slide directory
├── template/       # Template slide directory
└── themes
    ├── global.css  # Custom theme affecting the entire slide
    ├── index.css   # Entry point for the custom theme
    └── utility.css # Various utility classes used in the slides
```

## ✅ Requirements

| Tools                          | version |
|--------------------------------|---------|
| [Node.js](https://nodejs.org/) | 20.18.0 |
| [pnpm](https://pnpm.io/)       | 9.15.1  |

> [!tip]
> It is recommended to install Node.js using a version manager such as [nodenv](https://github.com/nodenv/nodenv).

## 🎉 Getting Started

### 0. Create a repository from the template

1. Create a repository by following the instructions in [Creating a repository from a template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template#creating-a-repository-from-a-template).
2. Change the repository settings according to the [documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow) to enable deployment from GitHubActions to GitHubPages.
3. Once the GitHub setup is complete, download the repository locally using $ git clone.

### 1. Repository Setup

- Change various settings such as URLs within the repository to match your ID and repository name.
- A [dedicated script](./scripts/init) is provided for easy modification.

```bash
$ scripts/init
```

- Follow the displayed instructions and enter your GitHub user ID and repository name.
  - Once entered, the script will automatically modify the settings.
- Change the language and timezone settings as needed.
  - The language setting is defined in [.marprc.yml](./.marprc.yml), and the timezone setting is specified in [.github/workflows/deploy.yml](./.github/workflows/deploy.yml).

> [!warning]
> The script uses the sed command.  
> It works fine on Mac (BSD), but on Linux (GNU), the option syntax differs, which may cause errors.  
> Linux (GNU) users should modify the [sed command in the script](https://github.com/yKicchan/awesome-marp-template/blob/main/scripts/init#L55-L66) as needed.

### 2. Install Dependencies

Install the dependencies to enable [markdown-it](https://github.com/markdown-it/markdown-it) plugins and [Marp CLI](https://github.com/marp-team/marp-cli).

```bash
$ pnpm install
```

### 3. Create a New Slide

- Create slides in the `src` directory.
- A [command](./scripts/new) is provided to easily create new slides from the [template](./template).

```bash
# Create a New Slide
$ pnpm new <slidename>
# If you want to group them, you can also split and create directories under src.
$ pnpm new path/to/<slidename>
```

The template slides to copy are located in the [template directory](./template).  
Feel free to customize them to suit your preferences!

### 4. Edit and Preview the Slide

Slides can be previewed in real-time in the browser using the features of [Marp CLI](https://github.com/marp-team/marp-cli).

```bash
# When editing slides under the src directory
$ pnpm dev
# When editing template slides
$ pnpm dev:tmp
```

> [!warning]
> This repository is extended using the [Engine](https://github.com/marp-team/marp-cli?tab=readme-ov-file#engine) feature of [Marp CLI](https://github.com/marp-team/marp-cli).  
> As a result, some features of the VSCode extension [`marp-vscode`](https://github.com/marp-team/marp-vscode) are not available.  
> For more details, refer to [@marp-team/marp-vscode/issues/85#issuecomment-543798586](https://github.com/marp-team/marp-vscode/issues/85#issuecomment-543798586).

That’s it for the basic usage! 🎉

## 🙌 Enjoy Marp even more! 🙌

Marp allows you to customize slide designs using the features of [Marpit](https://marpit.marp.app/).  
Additionally, you can extend the Markdown syntax using the [Engine](https://github.com/marp-team/marp-cli?tab=readme-ov-file#engine) feature of [Marp CLI](https://github.com/marp-team/marp-cli).

In this repository, customization is mainly done in the following two ways:

- Customizing the design and defining utility classes with CSS files in the [themes directory](./themes)
- Extending Markdown syntax using various plugins of [markdown-it](https://github.com/markdown-it/markdown-it)

Detailed usage for each is described below.

### Customizing the Theme

- Theme definitions are written in [themes/index.css](./themes/index.css).
- For example, edit this file if you want to change Marp's default theme or modify the syntax highlighting style (enabled by the integration of [`markdown-it-prism`](https://github.com/jGleitz/markdown-it-prism)).
- Additional custom themes that affect the entire slide are written in [themes/global.css](./themes/global.css).
- Edit this file to create your own unique theme!
- Convenient utility classes for slides are defined in [themes/utility.css](./themes/utility.css).
- For example, classes are added to change text sizes or to support element display in columns.
- A few useful CSS classes are provided by default, but feel free to customize them to suit your preferences!

> [!tip]
> The design of utility classes is inspired by [Tailwind CSS](https://tailwindcss.com/).

### Using Markdown Extended Syntax

Markdown extension settings are written in [engine.mjs](./engine.mjs).  
Recommended [markdown-it](https://github.com/markdown-it/markdown-it) plugins have been integrated.

- [`markdown-it-container`](https://github.com/markdown-it/markdown-it-container)
- [`markdown-it-attrs`](https://github.com/arve0/markdown-it-attrs)
- [`markdown-it-mark`](https://github.com/markdown-it/markdown-it-mark)
- [`markdown-it-ins`](https://github.com/markdown-it/markdown-it-ins)
- [`markdown-it-prism`](https://github.com/jGleitz/markdown-it-prism)
- [`markdown-it-textual-uml`](https://github.com/manastalukdar/markdown-it-textual-uml)

Please refer to the official documentation for each plugin.

## ✨The Ultimate Marp Slide Creation Technique ✨

Finally, let me introduce the ultimate combination of Markdown extended syntax and custom themes, which is the essence of this repository 💪  
You can check the actual display in the [demo slides](https://yKicchan.github.io/awesome-marp-template/demo).

### Assigning CSS Classes with `{.class}`

By using the [`markdown-it-attrs`](https://github.com/arve0/markdown-it-attrs) plugin, you can assign CSS classes to specific elements.

```markdown
This is a paragraph.{.gray}
```

This input will be converted to the following HTML.

```html
<p class="gray">This is a paragraph.</p>
```

The `.gray` class is a class defined in [themes/utility.css](./themes/utility.css) that changes the text color to gray.  
This allows you to easily apply styles to specific elements within the slide.  
It is also possible to specify multiple classes at the same time, as shown below.

```markdown
This is a small and gray paragraph.{.text-sm .gray}
```

### Decorating Specific Strings with `==` and `{.class}`

By combining [`markdown-it-mark`](https://github.com/markdown-it/markdown-it-mark) and [`markdown-it-attrs`](https://github.com/arve0/markdown-it-attrs), you can decorate specific strings only.

```markdown
This is a ==red=={.red} text.
```

This input will be converted to the following HTML.

```html
<p>This is a <mark class="red">red</mark> text.</p>
```

With [`markdown-it-mark`](https://github.com/markdown-it/markdown-it-mark), you can wrap specific strings with `==` to convert them into inline `<mark>` elements, and by applying a class to them, you can easily decorate only those specific strings.

### Change the style for each block with [`markdown-it-container`](https://github.com/markdown-it/markdown-it-container).

By enclosing with `:::`, you can change the style for each block.  
In this repository, `:::c` and `:::_` are predefined.

#### Display in columns with `:::c`

```markdown
:::c
Column 1

Column 2

Column 3
:::
```

This input will be converted to the following HTML.

```html
<div class="c">
  <p>Column 1</p>
  <p>Column 2</p>
  <p>Column 3</p>
</div>
```

The `.c` class is defined in [themes/utility.css](./themes/utility.css) as the `flex-container` setting.
This allows you to easily display elements in a column layout within the slide.

#### Use `:::_` for grouping.

```markdown
:::_
Group 1

Group 2

Group 3
:::
```

This input will be converted to the following HTML.

```html
<div class="_">
  <p>Group 1</p>
  <p>Group 2</p>
  <p>Group 3</p>
</div>
```
The `._` class is an **undefined dummy class**.  
A specific use case is when you want to apply a style to multiple elements at once, or when you want to group elements without changing their styles.

```markdown
:::_ {.blue}
This is a blue text.

This is a blue text.

This is a blue text.
:::
```

```markdown
::::c
:::_
## Left column
This is a left column text.
:::
:::_
## Right column
This is a right column text.
:::
::::
```

When nesting as shown above, you distinguish them by increasing the number of `:`.

### Display a filename in a code block with `{name=filename}`

This repository provides a feature that allows you to easily display a filename in a code block.  
By adding `{name=filename}` after the code block, you can display the filename.

````markdown
```js {name=index.js}
const message = "Thank you for using Awesome Marp Template!";
console.log(message);
```
````

The display will be as follows.

![Display a filename in a code block](https://github.com/user-attachments/assets/e4c5aee9-5ed1-4826-aa24-fe766c8426b1)

For the implementation details of this utility, please refer to [themes/utility.css](./themes/utility.css).

> [!warning]
> The implementation method may vary depending on the theme used by Marp.  
> If you are changing from the initial `gaia` theme in this repository, modifications are required.  
> Specifically, implementing it with the `default` theme can be quite challenging.  
> If you want to use this feature, it is recommended to either invent your own implementation method or select the `gaia` or `uncover` theme.

### Use Alert Design

This repository provides a feature to easily apply alert designs.  
By using the classes `.note`, `.important`, `.tip`, `.warning`, and `.caution`, you can apply alert designs.

![Alert Design](https://github.com/user-attachments/assets/98b1a1a5-4458-444d-a1a3-cececdc0d9c2)

---

That concludes the explanation of this repository!  
Feel free to use this template as a reference and enjoy creating slides that make the most out of Marp! ✨
