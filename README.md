# Website Documentation

This repository contains the source code for a personal website. The website consists of two main pages: `index.html` (the homepage) and `blog.html` (the blog page). Below is an explanation of the content and how to edit it.

## Files Overview

### `index.html`
- **Purpose**: The homepage of the website.
- **Structure**:
  - **Header**: Contains navigation links to the homepage and blog.
  - **Profile Picture**: Displays a profile image (`profile.png`) in a circular format.
  - **Bio Section**: Loads content from `bio.md` and converts it to HTML using Showdown.js.
  - **Papers Section**: Loads content from `papers.md` and converts it to HTML using Showdown.js.
- **Styling**: Uses an external stylesheet (`https://latex.vercel.app/style.css`) and includes custom CSS for the profile picture and layout.

### `blog.html`
- **Purpose**: The blog page of the website.
- **Structure**:
  - **Header**: Contains navigation links to the homepage and blog.
  - **Content Container**: Dynamically loads either a specific blog post or the blog index (`blog-index.md`) based on the URL query parameter `post`.
  - **Blog Posts**: Individual blog posts are stored as Markdown files in the `blog` folder and are loaded dynamically.
- **Styling**: Uses the same external stylesheet as `index.html`.

## How to Edit

### Editing Content
- **Bio**: Edit the `bio.md` file to update the bio section on the homepage.
- **Papers**: Edit the `papers.md` file to update the papers section on the homepage.
- **Blog Posts**:
  - Add new blog posts by creating Markdown files in the `blog` folder.
  - Update the `blog-index.md` file to include links to new blog posts.

### Editing Styles
- **Custom CSS**: Modify the `<style>` block in `index.html` to change the appearance of the profile picture or other elements.
- **External Stylesheet**: Replace the link to `https://latex.vercel.app/style.css` with a custom stylesheet if desired.

### Adding New Pages
- To add new pages, create new HTML files following the structure of `index.html` or `blog.html`. Ensure consistent navigation by including the same header and styles.

## Dependencies
- **Showdown.js**: Used for converting Markdown to HTML. Ensure the script is included in the HTML files:
  ```html
  <script src="https://cdn.jsdelivr.net/npm/showdown/dist/showdown.min.js"></script>
