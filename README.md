# Stread's Personal Website

This repository contains the source code for [stread.dev](https://stread.dev), my personal website built with [Hugo](https://gohugo.io/) and the [Bear Cub theme](https://github.com/clente/hugo-bearcub).

## Contributing

I welcome contributions to my blog! Whether it's fixing typos, improving grammar, suggesting content updates, or adding new blog posts/cheatsheets, your help is appreciated.

### How to Contribute

1. **Fork the Repository**
   - Click the "Fork" button at the top right of this repository
   - This creates a copy of the repository in your GitHub account

2. **Clone Your Fork**
   ```bash
   git clone https://github.com/YOUR-USERNAME/stread_website.git
   cd stread_website
   ```

3. **Create a Branch**
   ```bash
   git checkout -b your-branch-name
   ```
   
   Use a descriptive name like:
   - `fix-typo-linux-post`
   - `add-new-cheatsheet`
   - `update-project-info`

4. **Make Your Changes**
   - Edit existing files to fix errors
   - Add new content in the appropriate directories
   - For blog posts: `content/blog/`
   - For cheatsheets: `content/cheatsheets/`
   - For projects: `content/projects/`

5. **Preview Your Changes Locally**
   ```bash
   # Start the Hugo server with drafts enabled
   hugo server -D
   ```
   
   The site will be available at http://localhost:1313/

6. **Commit Your Changes**
   ```bash
   git add .
   git commit -m "Brief description of your changes"
   ```

7. **Push to Your Fork**
   ```bash
   git push origin your-branch-name
   ```

8. **Create a Pull Request**
   - Go to your fork on GitHub
   - Click "Pull Request"
   - Select your branch and describe your changes
   - Submit the pull request

9. **Add Yourself to Contributors**
   - When making a pull request, add yourself to the Contributors section at the end of this README
   - Follow the format shown in the Contributors section

### Content Guidelines

- All content should align with the minimal, clean aesthetic of the site
- Technical accuracy is important, especially for cheatsheets
- Respect the existing structure and formatting
- If adding new posts, include appropriate front matter (title, date, draft status)

### Technical Details

- The site is built with Hugo
- Content is written in Markdown
- Front matter is used for metadata (title, date, etc.)
- The site uses the Bear Cub theme
- Site structure:
  - `content/` - All content for the site
  - `content/_index.md` - Homepage content
  - `content/blog/` - Blog posts
  - `content/cheatsheets/` - Technical cheatsheets
  - `content/projects/` - Project descriptions
  - `content/about.md` - About page
  - `themes/hugo-bearcub/` - The Bear Cub theme
  - `hugo.yaml` - Site configuration

### Creating New Content

```bash
# Create a new blog post
hugo new content blog/my-post-name.md

# Create a new cheatsheet
hugo new content cheatsheets/my-cheatsheet.md

# Create a new project page
hugo new content projects/my-project.md
```

Thank you for helping improve stread.dev!

## Contributors

This section recognizes those who have contributed to the project. If you make a contribution, please add yourself to this list in your pull request.

- **[Your Name](https://github.com/your-username)** - *Contribution description* - Date
- **Example:** [John Doe](https://github.com/johndoe) - Fixed typos in Linux blog post - July 2023 