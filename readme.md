# react-nginx-docker-template

This repository provides a clean Docker setup for serving a React application with a lightweight Nginx server, specifically configured to solve common routing issues.

## Overview

This project provides a pre-configured Nginx image that is specifically optimized to solve a common problem with single-page applications: 404 errors on page refreshes and direct URL access.

By using this image, you can ensure that your application’s client-side routing works as expected in a production environment, sending all unhandled requests back to your main index.html file.

## Getting Started

Follow these steps to build and run your React application using this template.

1. Build Your React Application

First, navigate to your React project's root directory and run the build command to generate the static files.

```
npm run build
```

This will create a dist (or build) folder containing your production-ready files.

2. Build the Custom Nginx Image

Next, navigate to the directory where you saved the Dockerfile and nginx.conf files from this repository. Build your custom Nginx image with the following command:

```
docker build -t your-custom-nginx .
```

This command creates a new Docker image named your-custom-nginx that is configured to serve single-page applications.

3. Run the Docker Container

Finally, you can run a container from your new image and serve your React application's built files. The -v flag creates a volume mount, linking your local build directory to the Nginx server's document root inside the container.

```
docker run -p 8080:80 -v /path/to/your/react/project/dist:/usr/share/nginx/html your-custom-nginx
```

Note: Replace /path/to/your/react/project/dist with the actual absolute path to your React app's dist or build folder.

Open your browser and navigate to http://localhost:8080 to see your application running. All client-side routes will now work correctly.

## Troubleshooting

If you see a page with the title "Project Configuration Error" when you navigate to your application, it means the volume mount was not set up correctly. This page is the default index.html from the Nginx container, indicating that your application's files were not copied over.

To fix this, double-check that the path in your docker run command is correct and points to the location of your built files (e.g., dist or build folder).
