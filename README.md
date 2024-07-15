# Node.js Cloud Native Buildpack

This repository contains a simple Node.js buildpack for transforming Node.js source code into a runnable container image. The buildpack handles downloading and setting up Node.js, and setting the process type for running the application.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Pack CLI](https://buildpacks.io/docs/tools/pack/): A CLI tool for working with buildpacks

## Buildpack Structure

- **bin/**: Contains the `build` and `detect` scripts for the buildpack.

## File Structure
```
nodejs_buildpack/
├── bin/
│ ├── build
│ └── detect
└── README.md
```

## Using the Buildpack

1. Create a test Node.js application:

    ```sh
    mkdir test-app
    cd test-app
    npm init -y

    Add code mentioned below in app.js:

    const http = require('http');
    const hostname = '0.0.0.0';
    const port = 8080;
    
    const server = http.createServer((req, res) => {
      res.statusCode = 200;
      res.setHeader('Content-Type', 'text/plain');
      res.end('Welcome to buildpacks!');
    });
    
    // Start the server
    server.listen(port, hostname, () => {
      console.log(`Server running at http://${hostname}:${port}/`);
    });
    ```

2. Build the application using the Pack CLI:

    ```sh
    pack build my-nodejs-app --path ./test-app --buildpack ./nodejs_buildpack
    ```

3. Run the built Docker image:

    ```sh
    docker run --rm -p 8080:8080 my-nodejs-app
    ```

This will download Node.js, set it up, and package your application into a runnable Docker image.

## Conclusion

This Node.js buildpack simplifies the process of building the nodejs applications. By automating the download and setup of Node.js, it ensures consistency and efficiency in the build process.

For more information, refer to the [official Buildpacks documentation](https://buildpacks.io/docs/).
