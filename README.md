
# Mango

Mango is a clean, fast, and responsive Hugo theme designed for blogging and personal websites. It features a modern dark/light theme toggle, mobile-friendly navigation, and a focus on readability and performance.

![Mango Theme Screenshot](https://raw.githubusercontent.com/manikandaraj/mango/main/images/screenshot.png)

## Features

* **Responsive Design**: Optimized for desktop, tablet, and mobile devices
* **Dark/Light Theme**: Automatic theme switching with manual toggle option
* **Mobile Navigation**: Collapsible hamburger menu for mobile devices
* **Fast Performance**: No external dependencies, minimal JavaScript
* **SEO Optimized**: Clean markup and meta tags for better search engine visibility
* **Social Links**: Integrated social media links (GitHub, LinkedIn, Twitter, Stack Overflow)
* **Syntax Highlighting**: Beautiful code highlighting for technical blogs
* **Clean Typography**: Readable fonts and proper spacing for better reading experience

## Installation

### Git Submodule (Recommended)

Add Mango as a submodule to your Hugo site:

```bash
git submodule add https://github.com/manikandaraj/mango.git themes/mango
```

### Manual Download

1. Download the theme from the [releases page](https://github.com/manikandaraj/mango/releases)
2. Extract to `themes/mango` in your Hugo site directory

## Configuration

Update your `config.toml` file:

```toml
baseURL = 'https://yourdomain.com'
languageCode = 'en-us'
title = 'Your Site Title'
theme = "mango"

[params]
copyright = "© 2024 Your Name. All rights reserved."

# Social Network Links
[params.social]
github = "https://github.com/yourusername"
linkedin = "https://linkedin.com/in/yourusername"
twitter = "https://x.com/yourusername"
stackoverflow = "https://stackoverflow.com/users/youruser"

# Theme Colors (Optional - defaults provided)
[params.colors]
accent_color = "#64ffda"
# ... more color options available

# Navigation Menu
[[menu.main]]
name = "Home"
url = "/"
weight = 1

[[menu.main]]
name = "About"
url = "/about"
weight = 2

[[menu.main]]
name = "Blog"
url = "/posts"
weight = 3
```

## Usage

### Creating Content

Create new blog posts:

```bash
hugo new posts/my-new-post.md
```

Create new pages:

```bash
hugo new about.md
```

### Running the Site

Start the development server:

```bash
hugo server -D
```

Build for production:

```bash
hugo
```

## Customization

The theme supports extensive customization through the `config.toml` file:

- **Colors**: Customize theme colors for both dark and light modes
- **Social Links**: Add your social media profiles
- **Navigation**: Configure header menu items
- **Advertisement**: Set custom banner sizes

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This theme is released under the MIT License. See [LICENSE](LICENSE) for details.

## Support

If you encounter any issues or have questions, please [open an issue](https://github.com/manikandaraj/mango/issues) on GitHub.

## Author

**Manikandaraj Srinivasan**
- Website: [manikandaraj.com](https://manikandaraj.com)
- GitHub: [@manikandaraj](https://github.com/manikandaraj)
