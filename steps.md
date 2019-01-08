Create a New Repository - hicarlos.eu

Clone the Repository on the computer
**git clone https://github.com/Carlosmcoelho/hicarlos.eu.git && cd hicarlos.eu**

Make your website work locally (**hugo server** or hugo server -t <YOURTHEME>) and open your browser to http://localhost:1313.
  
Once you are happy with the results:
- Press Ctrl+C to kill the server
- **rm -rf public** to completely remove the public directory

**git submodule add -b master git@github.com:Carlosmcoelho/Carlosmcoelho.github.io.git public**. 
This creates a git submodule. Now when you run the hugo command to build your site to public, the created public directory will have a different remote origin (i.e. hosted GitHub repository). You can automate some of these steps with the following script.

You can also add a **deploy.sh** script to automate the preceding steps for you. You can also make it executable with **chmod +x** **deploy.sh**.
```
cd folderpaht
touch deploy.sh
```
Open file on text editor.

The following are the contents of the **deploy.sh** script:
```
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..
```
You can then run ./deploy.sh "Your optional commit message" to send changes to <USERNAME>.github.io. Note that you likely will want to commit changes to your <YOUR-PROJECT> repository as well.

That’s it! Your personal page should be up and running at https://<USERNAME>.github.io within a couple minutes.

**Github Project Page**:
Make sure your baseURL key-value in your site configuration reflects the full URL of your GitHub pages repository if you’re using the default GH Pages URL (e.g., <USERNAME>.github.io/<PROJECT>/) and not a custom domain.

Deployment of Project Pages from Your master Branch 
To use master as your publishing branch, you’ll need your rendered website to live at the root of the GitHub repository. Steps should be similar to that of the gh-pages branch, with the exception that you will create your GitHub repository with the public directory as the root. Note that this does not provide the same benefits of the gh-pages branch in keeping your source and output in separate, but version controlled, branches within the same repo.

You will also need to set master as your publishable branch from within the GitHub UI:

Go to Settings → GitHub Pages
From Source, select “master branch” and then Save.

Use a Custom Domain 
If you’d like to use a custom domain for your GitHub Pages site, create a file static/CNAME. Your custom domain name should be the only contents inside CNAME. Since it’s inside static, the published site will contain the CNAME file at the root of the published site, which is a requirements of GitHub Pages.

Refer to the official documentation for custom domains for further information.


reference 
https://github.com/luizdepra/luizdepra.com
