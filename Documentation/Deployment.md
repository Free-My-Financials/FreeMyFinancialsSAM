# Deployment

1. To deploy on a cloud service such as Netlify is required.
2. Using Netlify, you must first create an account.
3. Add a new site, using the import in existing project button.
4. Link your github to Netlify by clicking the deploy with github button.
5. Select the repo that contains the Free My Financials project.
6. With options, first select the branch to deploy, with the original free-my-financials project, that branch would be main.
7. Base directory needs to be set to web.
8. Build command is npm run build
9. Publish directory is web/dist
10. Then click the deploy button.

# Points of failure
Critical pieces that can fail are cookie storage and adding transactions to make the total.

# Logging
Check the build logs to see if issues arise