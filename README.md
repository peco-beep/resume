# Hosting a Markdown Resume on a Forge with Pelican

Want to host your resume online? This guide provides a step-by-step process to create a simple Markdown resume and publish it using a forge with static site hosting.

## Purpose
This instruction provides a step-by-step guide on how to format and host a resume that is made by using Markdown then use a forge that offers static web hosting. It is designed for users who are new to Git, static site generators, and online forges. 


## Prerequisites
Before continuing this guide, ensure you have the following:

- A Machine running Windows
- A basic understanding of Markdown
- Git installed on your system ([Download Git](https://git-scm.com/downloads))
- A GitHub account ([Sign up here](https://github.com/))
- A text editor such as VS Code ([Download VS Code](https://code.visualstudio.com/)) or any other text editor
- Python installed on your PC ([Download Python](https://www.python.org/downloads/))
   - During installation, ensure you check the box **Add Python to PATH** or **Add Python to environment variables**

## Instructions

   - **Note**: if commands like `pelican` or `ghp-import` do not work, try restarting VS Code

### 1. Make Your Resume using Markdown

1. Open VS Code.
2. Create a new file and name it `resume.md` (or some other name).
3. Create your first resume using markdown. Here is an example to get you started
   ```md
   Title: Resume
   Date: DD-MMMM-YYYY 
   
   # John Doe
   **Manager**  
   Email: email@example.com  
   
   ## Experience
   - **management** at foomatic Corp (yyyy-yyyy)
  
   ## Education
   - **Bachelor of foom**, University of foomatic (yyyy-yyyy)
   
   ## Skills
   - management
   ```

4. Save the file in an easily accessible folder.

   **Note**: the title and are necessary because pelican need that data for generating the website

You might wonder why Markdown is preferred for documentation. Well according to the book, "modern technical writing", by Andrew Etter, Markdown is a `lightweight markup languages`, meaning it's easy to read, write, and maintain without requiring special tools. It is ideal for technical documentation because it allows you focus more on **writing** instead **formatting**.

### 2. Create a GitHub Repository and clone it into your PC

1. Log into your [GitHub account](https://github.com/).
2. Click the **+** icon in the top-right and select **New repository**.
3. Name your repository (e.g., `resume`).
4. set it to public.
5. Click **Create repository**.
6. Open VS Code
7. Open the terminal
   - If the terminal is not there, click the **Terminal** in the top left and click **New Terminal**
8. Clone your repository (you can copy the link of the repository)
   ```sh
   git clone https://github.com/username/resume
   ```

If you are new to Git, it may seem confusing at first. However, as Etter stated, Git enables multiple contributors to collaborate efficiently without overwriting each other’s work.

### 3. Using Pelican to generate a static website

Pelican is a static site generator that converts Markdown files into a website. 

1. Go back to the terminal and install pelican with markdown support
   ```sh
   python -m pip install "pelican[markdown]"
   ```
2. Navigate to your cloned repository
   ```sh
   cd resume
   ```
3. Run pelican quickstart to create a website
   ```sh
   pelican-quickstart
   ```
4. Input each prompt based on what you want
   - **Note**: in the example I showed, any empty input that is entered means that it will be set to a default value. Also, the URL prefix need to have this template **(`https://username.github.io/resume`)**, where the `username` will be your github username. and `resume` will be your repo or project folder name

   ```sh
   > Where do you want to create your new web site? [.]
   > What will be the title of this web site? (any name for the title but just put resume)
   > Who will be the author of this web site? (your name)
   > What will be the default language of this web site? [English] 
   > Do you want to specify a URL prefix? e.g., https://example.com   (Y/n) y
   > What is your URL prefix? (see above example; no trailing slash) https://username.github.io/resume 
   > Do you want to enable article pagination? (Y/n) 
   > How many articles per page do you want? [10] 
   > What is your time zone? [Europe/Rome] "Continent/City"(Ex: America/Winnipeg)
   > Do you want to upload your website using SSH? (y/N)
   > Do you want to upload your website using Dropbox? (y/N)
   > Do you want to upload your website using S3? (y/N)
   > Do you want to upload your website using Rackspace Cloud Files? (y/N)
   > Do you want to upload your website using GitHub Pages? (y/N)
   ```
   *You can find the list of timezone in the further resources section*

As Andrew Etter mentions in Modern Technical Writing, static websites have many advantages, such as speed, simplicity, portability, and security. Also, it's easy to update and maintain your website by simply modifying the content and reprocessing it.

### 4. Hosting your website in Github

   We have arrived to the final part of the instruction, how to properly host a website in Github.

   1. Copy `resume.md` into the `content` folder inside your `resume` folder.
   2. Install ghp-import in the terminal.
   ```sh
   python -m pip install ghp-import
   ```
   3. Stage your files ("Ensure your terminal is inside the correct project directory, `path\to\your\comp project\resume`).
   ```sh
   git add .
   ```
   4. Commit the files into your repository.
   ```sh
   git commit -am "first commit"
   ```
   5. Generate your website 
   ```sh
   pelican content -s publishconf.py
   ```
   6. Upload it into to Github
   ```sh
   ghp-import output -b gh-pages
   git push origin gh-pages
   ```
   7. Go back to your Github account and find the `resume` repository, it should have all the files the you have uploaded
   8. Go to **Settings**, click **Pages** and make sure the **source** is `deploy from branch` and **branch** is `gh-pages`
   9. Go to your newly hosted website with the url `https://username.github.io/resume`

You might ask, "why use Github for hosting the web?", well GitHub is free and Etter mentioned that it provides a structured workflow for collaborative documentation.
   
## Further Resources/Readings
For additional resources and further reading, consider these:

- [Markdown Guide](https://www.markdownguide.org/) - A guide to Markdown syntax.
- [Markdown tutorial](https://commonmark.org/help/tutorial/) -  Tutorial for understanding the syntax in markdown
- [GitHub Pages Documentation](https://docs.github.com/en/pages) - Official GitHub documentation.
- [Git documentation](https://git-scm.com/docs)
- [tz database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) - List of timezone that can used website generation.
- [cv template](https://github.com/casualwriter/casual-markdown-cv) - For a more detailed template for your resume.
- [web themes](https://github.com/getpelican/pelican-themes) - Additional themes for the website and how to use them.
- [Pelican documentation](https://docs.getpelican.com/en/latest/)

## FAQ

### Why is Markdown better than writing raw HTML?
Markdown is preferred because it is lightweight, easy to read, and does not require extensive knowledge of HTML. 

### I changed the Markdown version of my resume, so why don’t I see the changes when I refresh the website in my browser?
If you made changes to your `resume.md` file but don’t see updates, try the following:
1. Commit your changes to GitHub:
   ```sh
   cd content
   git add resume.md
   git commit -m "Updated resume"
   cd ..
   ```
2. Run these command lines again:
    ```sh
   pelican content -s publishconf.py
   ghp-import output -b gh-pages
   git push origin gh-pages
   ```
3. Wait for a few minutes and try refreshing your website. It should be updated properly

### Why does my website have no CSS styling after deployment?
1. Open `pelicanconf.py` in your repo folder.
2. Update `SITEURL`.
   ```sh
   SITEURL = "https://username.github.io/example/"`
   ```
3. Run these command lines again:
    ```sh
   pelican content -s publishconf.py
   ghp-import output -b gh-pages
   git push origin gh-pages
   ```
4. Wait for a few minutes and try refreshing your website. It should be updated properly

**Note**: Github caches assets aggressively, so changes might not appear immediately. If that happen press `Ctrl + Shift + R`

## Credits

   - [modern technical writing by andrew etter](https://www.amazon.com/Modern-Technical-Writing-Introduction-Documentation-ebook/dp/B01A2QL9SS)
   - [William S. Pfeiffer’s Technical Communication](https://www.amazon.com/Technical-Communication-Practical-Approach-8th/dp/0132785781)
   - [MrSenko](https://github.com/MrSenko/pelican-octopress-theme/tree/29020e048cadefffc8825e571593b88be26f22bc) - theme for the website
   - My group members that helped me peer reviewed this project:
      - Ty Bryant
      - Minh Do