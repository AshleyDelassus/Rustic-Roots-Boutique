import os
import zipfile

# Recreate enhanced website structure after state reset
website_files = {
    "index.html": """<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="A simple, elegant website built with HTML and CSS.">
    <meta name="keywords" content="HTML, CSS, Website, GitHub Pages, Portfolio">
    <meta name="author" content="Your Name">
    <link rel="icon" href="favicon.ico" type="image/x-icon">
    <title>My Website</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Welcome to My Website!</h1>
    <p>This is a sample site ready to be published via GitHub Pages.</p>
</body>
</html>""",
    "style.css": """body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    color: #333;
    text-align: center;
    margin-top: 50px;
}""",
    "README.md": """# My Website

Welcome to **My Website** – a simple static site built with HTML and CSS.

## Features
- Clean, responsive design
- Easy to publish using GitHub Pages
- Lightweight and fast

## How to Publish
1. Upload all files to a public GitHub repository.
2. Go to **Settings > Pages**.
3. Select the **main branch** and save.
4. Your site will be live at `https://yourusername.github.io/repo-name`.

---

Feel free to customize and expand this site as you like!
"""
}

# Create directory
base_path = "/mnt/data/my_website"
os.makedirs(base_path, exist_ok=True)

# Write files to disk
for filename, content in website_files.items():
    with open(os.path.join(base_path, filename), 'w') as f:
        f.write(content)

# Add dummy favicon
favicon_path = os.path.join(base_path, "favicon.ico")
with open(favicon_path, "wb") as f:
    f.write(b"\x00\x00\x01\x00\x01\x00\x10\x10\x00\x00\x01\x00\x04\x00\x28\x01\x00\x00" + b"\x00" * 100)

# Zip all files
zip_path = "/mnt/data/my_website.zip"
with zipfile.ZipFile(zip_path, 'w') as zipf:
    for filename in list(website_files.keys()) + ["favicon.ico"]:
        zipf.write(os.path.join(base_path, filename), arcname=filename)

zip_path
