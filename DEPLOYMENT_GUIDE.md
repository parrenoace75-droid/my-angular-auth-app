# Deployment Guide

This guide will walk you through deploying this full-stack application (Angular frontend + Express/Node.js backend) on Vercel. 

Because we have restructured the repository to align with Vercel's standard layout and moved secrets to environment variables, deployment is straightforward.

## 1. Push to GitHub, GitLab, or Bitbucket
Ensure your codebase is pushed to a remote Git repository. Vercel integrates natively with these platforms for continuous deployment.

## 2. Import your Project into Vercel
1. Log in to your [Vercel Dashboard](https://vercel.com/dashboard).
2. Click the **Add New...** button and select **Project**.
3. Import the repository you just pushed.
4. In the **Configure Project** section:
   - **Framework Preset**: Vercel should automatically detect `Angular`. Leave it as is.
   - **Root Directory**: Leave it as `./` (the root).
   - **Build and Output Settings**: Vercel will auto-fill the build command (`ng build`) and the output directory (usually `dist/<project-name>`).

## 3. Set Up Environment Variables
Before clicking "Deploy", you must provide the Environment Variables your Node.js backend requires to function correctly (for the database, email, and JWT). 

In the **Configure Project** section, expand the **Environment Variables** tab and add the following keys and values:

### Database (MySQL)
To host your database in the cloud, consider providers like **PlanetScale**, **Aiven**, or **Railway** which offer managed MySQL databases. Once you have a cloud DB, add its connection details:
- `DB_HOST`: The hostname of your cloud database (e.g., `aws.connect.psdb.cloud`)
- `DB_PORT`: The port (default is usually `3306`)
- `DB_USER`: Your database username
- `DB_PASSWORD`: Your database password
- `DB_NAME`: The name of the database

### Authentication (JWT)
- `JWT_SECRET`: A secure random string for signing JWT tokens.

### Email (Nodemailer via Gmail or other SMTP)
- `SMTP_HOST`: `smtp.gmail.com` (or your provider's host)
- `SMTP_PORT`: `465` (or `587`)
- `SMTP_USER`: Your email address (e.g., `you@gmail.com`)
- `SMTP_PASS`: Your App Password (For Gmail, generate an App Password in your Google Account security settings)
- `EMAIL_FROM`: The address emails will be sent from (e.g., `you@gmail.com`)

## 4. Deploy
Once all variables are added, click **Deploy**. Vercel will build your Angular application and automatically set up your Node.js API based on the `api/` folder and `vercel.json` configuration.

After the build is complete, you will receive a public URL. Any request to `/api/*` will route to your Express backend, while any other request will serve your Angular frontend.
