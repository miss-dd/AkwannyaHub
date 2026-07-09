# Akwannya Hub

Akwannya Hub is a static portfolio website built with Vite, React, and Tailwind CSS. The site is deployed to AWS S3 and served through a continuous deployment pipeline powered by GitHub Actions.

## Project Structure

```
akwannya-hub/
  assets/           Images, logos, and static media
  css/              Source stylesheets (Tailwind)
  js/               Source JavaScript
  src/              Application source code
  node_modules/     Installed dependencies (not committed)
  about.html
  contact.html
  faq.html
  index.html
  programs.html
  projects.html
  team.html
  metadata.json
  package.json
  tsconfig.json
  vite.config.ts
```

## Tech Stack

Vite as the build tool, React for interactive components, Tailwind CSS for styling, and Node.js version 20 or higher required for the build process.

## Getting Started

Clone the repository and install dependencies.

```bash
git clone https://github.com/your-username/akwannya-hub.git
cd akwannya-hub
npm install
```

Run the development server.

```bash
npm run dev
```

Build the project for production.

```bash
npm run build
```

The build output is generated in the `dist` folder. This is the folder that gets deployed, not the raw source files.

## Deployment

The site is hosted on AWS S3 using static website hosting. Deployment happens automatically through a GitHub Actions workflow whenever changes are pushed to the main branch.

### Manual Deployment

If a manual deployment is needed, build the project first, then sync the output to S3.

```bash
npm run build
aws s3 sync dist s3://akwannya-hub-portfolio --delete
```

The `--delete` flag removes files from the bucket that no longer exist in the build output, keeping the bucket in sync with the latest build.

### Automated Deployment (CI/CD)

The GitHub Actions workflow located at `.github/workflows/deploy.yml` runs on every push to main. It performs the following steps in order: checks out the repository, sets up Node.js version 20, installs dependencies, builds the project, configures AWS credentials, and syncs the build output to the S3 bucket.

The following secrets must be configured in the repository settings under Secrets and Variables for Actions.

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_REGION
S3_BUCKET
```

## Important Notes

The `css/style.css` file contains a Tailwind CSS import directive and is not valid standalone CSS. It must be processed through the build step before deployment. Do not upload raw source files directly to S3; always deploy the contents of the `dist` folder.

The `node_modules` folder should never be uploaded to S3 or committed to the repository. It is excluded through `.gitignore` and should also be excluded from any manual S3 sync commands.

This project should be run from a native Linux file system when using Windows Subsystem for Linux. Running the build from a Windows mounted path such as `/mnt/c/...` has caused native dependency resolution errors in the past.

## License

Add license information here.
