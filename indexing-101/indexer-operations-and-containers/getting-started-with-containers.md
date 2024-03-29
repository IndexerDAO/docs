# Container overview
A **container** is a lightweight, standalone executable package that contains everything an application needs to run, including code, libraries, dependencies, and system tools. Containers are designed to be portable, scalable, and isolated from the host system and other containers.

**Key concepts**
* **Image**: An image is a read-only template that defines the application and its dependencies.
* **Container**: A container is a runtime instance of an image. It is isolated from other containers and the host system, and has its own file system, network interfaces, and resources.
* **Registry**: A registry is a repository for storing and distributing container images. The most popular registry is [Docker Hub](https://hub.docker.com/), but you can also use private registries for storing images.

**Benefits of containers**
* **Portability**: Containers can run on any platform that supports containerization, from laptops to cloud servers. This makes it easy to move applications between development, testing, and production environments.
* **Isolation**: Containers are isolated from the host system and other containers, which makes them more secure and less prone to conflicts.
* **Efficiency**: Containers are lightweight and share the host system's resources, which makes them more efficient than traditional virtual machines.

**Drawbacks of containers**
* **Limited resource allocation**: Containers share the resources of the host system, which means that each container has a limited amount of CPU, memory, and disk space. This can become a problem if an application requires more resources than the container can provide.
* **Security concerns**: Containers are isolated from the host system and other containers, but they still share the same kernel as the host system. This can create potential security risks, especially if the container has vulnerabilities or is misconfigured.
* **Complexity**: Containers add an extra layer of complexity to software development and deployment. You need to manage the container runtime, container images, container networking, and container orchestration, which can be challenging if you're not familiar with these technologies.
* **Debugging difficulties**: Debugging applications in containers can be more difficult than debugging applications on the host system. You need to understand how the container runtime and container networking work to troubleshoot issues effectively.
* **Dependency management**: While containers help manage dependencies by bundling everything an application needs to run, they can also introduce dependency management issues. If two containers require different versions of the same library, for example, you'll need to find a way to resolve the conflict.

While [Docker](https://www.docker.com/) is the most popular container technology, there are other containerization technologies, such as [LXC/LXD](https://linuxcontainers.org/lxd/introduction/), [CRI-O](https://cri-o.io/), and [containerd](https://containerd.io/). Each technology has its own strengths and weaknesses, but the basic concept of containerization remains the same: encapsulating applications and their dependencies into a self-contained unit that can run consistently across different environments. 

Containers can be managed using container orchestration platforms like [Kubernetes](https://kubernetes.io/) or [Docker Swarm](https://docs.docker.com/get-started/swarm-deploy/). These platforms provide a way to deploy, scale, and manage containers across multiple hosts, making it easier to build and run complex applications.




## Running single container applications with `docker`
Docker provides a simple and efficient way to run single container applications in a consistent and reproducible way. Running a single container application with Docker involves creating a Docker image, which is a packaged, self-contained unit that includes the application code and its dependencies, and then running a container based on that image. Docker images can be built locally or pulled from a registry like Docker Hub, and containers can be run on any platform that supports Docker, from local development environments to production servers. Docker also provides a range of features for managing and monitoring containers, making it easy to deploy and manage single container applications at scale.


### Toy example
Let's demonstrate to generic workflow for running an app with `docker`
1. **Create a Dockerfile**: A Dockerfile is a text file that contains instructions for building a Docker image. You'll need to create a Dockerfile for your application.
2. **Build the Docker image**: Once you've created your Dockerfile, you can use the docker build command to build a Docker image from it. This will create an image that includes your application and its dependencies.
    ``` bash
    docker build -t myapp .
    ```
    > Note: This command will build an image from the Dockerfile in the current directory and tag it with the name `myapp`.

3. **Run the Docker container**: Once you've built the Docker image, you can use the docker run command to start a container from the image.
    ``` bash
    docker run -p 8080:80 myapp
    ```
    > Note: This command will start a container from the `myapp` image and map port `80` in the container to port `8080` on the host system.

4. **Access your application**: Once your container is running, you can access your application by navigating to [http://localhost:8080](http://localhost:8080) in your web browser. If your application is not a web application, you'll need to use the appropriate method for accessing it.

### Weather application
Let's build a single container Rust application that gets the current weather in Los Angeles, California. Requires a local installation of Rust ([installation instructions available here](https://www.rust-lang.org/tools/install)).
1. **Choose a weather API**: There are many weather APIs available, some of which are free and some of which require payment or registration. One popular free API is OpenWeatherMap. You'll need to sign up for an account and get an API key to use their service.
1. **Create a new Rust project**: You can create a new Rust project using the cargo new command
    ``` bash
    cargo new weather-app
    ```
   > Note: This will create a new directory called weather-app with a basic Rust project structure.
 
1. **Add dependencies**: You'll need to add dependencies to your `Cargo.toml` file for the `reqwest` library, which will be used to make HTTP requests to the weather API, and `serde` and `serde_json` libraries to deserialize the JSON response.

    ``` toml
    [dependencies]
    reqwest = { version = "0.11", features = ["json"] }
    serde = { version = "1.0", features = ["derive"] }
    serde_json = "1.0"
    ```

1. **Write the Rust code**: You'll need to write the Rust code that makes an API request to the weather API and prints the current weather in Los Angeles.
    ``` rust
    use serde::{Deserialize, Serialize};

    #[derive(Serialize, Deserialize)]
    struct WeatherResponse {
        weather: Vec<Weather>,
        main: Main,
    }

    #[derive(Serialize, Deserialize)]
    struct Weather {
        description: String,
    }

    #[derive(Serialize, Deserialize)]
    struct Main {
        temp: f32,
    }

    #[tokio::main]
    async fn main() -> Result<(), Box<dyn std::error::Error>> {
        let api_key = std::env::var("API_KEY").expect("API_KEY environment variable not set");
        let url = format!("http://api.openweathermap.org/data/2.5/weather?q=Los+Angeles,California&units=imperial&appid={}", api_key);
        let res = reqwest::get(&url).await?.json::<WeatherResponse>().await?;
        let temp = res.main.temp;
        let description = res.weather[0].description.clone();
        println!("The current weather in Los Angeles, California is {} and the temperature is {} degrees Fahrenheit", description, temp);
        Ok(())
    }
    ```
    > Note: This code defines structs for the JSON response from the weather API, makes an HTTP GET request to the API with the appropriate API key and query parameters, deserializes the JSON response into the defined structs, and prints the current weather in Los Angeles to the console.

1. **Write the Dockerfile**: You'll need to write a Dockerfile that specifies the base image, copies your Rust code into the container, installs the Rust toolchain and dependencies, and builds your application.

    ``` dockerfile
    # Use the official Rust image as the base image
    FROM rust:latest

    # Create a new directory inside the container
    WORKDIR /usr/src/weather-app

    # Copy the contents of the local directory into the container
    COPY . .

    # Install any required dependencies
    RUN apt-get update && apt-get install -y openssl

    # Build the application
    RUN cargo build --release

    # Run the application
    CMD ["./target/release/weather-app"]
    ```
    > Note: This Dockerfile starts with the official Rust image as the base, creates a new working directory inside the container, copies the contents of the local directory into the container, installs any required dependencies, builds the application in release mode, and sets the default command to run the built application.

1. **Build the Docker image**: You can build the Docker image using the following command:

    ``` bash
    docker build -t weather-app .
    ```
    > Note: This will build a Docker image with the tag weather-app using the Dockerfile in the current directory.


1. **Run the Docker container**: You can run the Docker container using the following command:
    ``` bash
    docker run -e API_KEY=YOUR
    ```

## Running multi-container applications
Running multi-container applications with [Docker Compose](https://docs.docker.com/compose/), [Kubernetes](https://kubernetes.io/), and [Helm](https://helm.sh/) are three popular approaches for managing complex containerized applications. Docker Compose is best suited for small to medium-sized applications that run on a single host, providing a simple way to define and manage the entire stack of containers. Kubernetes is a container orchestration platform that is designed for large-scale production deployments, with support for scaling, load balancing, and self-healing capabilities. Kubernetes is more complex to set up and manage than Docker Compose, but it provides greater flexibility and resilience for large applications that need to scale. Helm is a package manager for Kubernetes that simplifies the deployment of complex applications by providing a templating system for defining Kubernetes resources, making it easier to deploy and manage applications. Helm charts can be used to define application dependencies and can be versioned and shared with others, making it easier to collaborate on complex deployments. Overall, the choice of whether to use Docker Compose, Kubernetes, or Helm depends on the complexity and scale of the application, as well as the specific requirements of the development team.

### `docker-compose`
Docker Compose is a tool for defining and running multi-container Docker applications. It allows developers to define their application stack in a declarative YAML file, specifying the containers, their dependencies, and configuration options. Docker Compose can then start, stop, and manage these containers as a single unit, making it easy to develop, test, and deploy complex multi-container applications. With Docker Compose, developers can create an isolated development environment with multiple services running in different containers, each with its own environment variables, networking, and volumes. Docker Compose also supports scaling containers, managing data volumes, and defining custom network configurations. Overall, Docker Compose simplifies the process of managing multi-container applications, making it easier to build, test, and deploy complex applications with Docker.

#### Toy example
Coming soon

### Kubernetes
Coming soon

### Helm
Coming soon
