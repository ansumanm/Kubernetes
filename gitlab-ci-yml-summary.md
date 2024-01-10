# .gitlab-ci.yml file summary

1. **Stages**: Define the stages in your pipeline (like build, test, deploy). Jobs are grouped into these stages.
   ```yaml
   stages:
     - build
     - test
     - deploy
   ```

2. **Jobs**: Each job represents a set of commands that are executed by the runner. Jobs are defined under stages.
   ```yaml
   build_job:
     stage: build
     script:
       - echo "Building the application..."
       - build_script.sh

   test_job:
     stage: test
     script:
       - echo "Running tests..."
       - test_script.sh
   ```

3. **Image**: Specifies the Docker image to use for the runner's environment.
   ```yaml
   image: ruby:2.7
   ```

4. **Script**: Contains commands that are executed by the runner. These can be build commands, test commands, etc.
   ```yaml
   script:
     - echo "Hello, world!"
   ```

5. **Only/Except**: Defines rules to limit when jobs are created. You can specify branches or tags.
   ```yaml
   only:
     - master
   except:
     - develop
   ```

6. **Artifacts**: Files created by jobs that are passed to subsequent stages.
   ```yaml
   artifacts:
     paths:
       - build/
   ```

7. **Cache**: Used to specify a list of files and directories which should be cached between jobs.
   ```yaml
   cache:
     paths:
       - node_modules/
   ```

8. **Before_script and After_script**: Commands that are run before and after each job's script.
   ```yaml
   before_script:
     - setup_script.sh
   after_script:
     - cleanup_script.sh
   ```

9. **Variables**: Define variables that can be used in the job environment.
   ```yaml
   variables:
     DATABASE_URL: "postgres://postgres:password@postgres/mydatabase"
   ```

10. **Services**: Use Docker services like databases that are linked to the Docker container where the job is run.
    ```yaml
    services:
      - postgres:latest
    ```

11. **Include**: Include external YAML files. Useful for reusing configurations across projects.
    ```yaml
    include:
      - project: 'my-group/my-project'
        ref: master
        file: '/templates/template.yml'
    ```

12. **Full Example**:
    ```yaml
    stages:
      - build
      - test
      - deploy

    build_job:
      stage: build
      script:
        - echo "Building the application..."
        - build_script.sh
      only:
        - master

    test_job:
      stage: test
      script:
        - echo "Running tests..."
        - test_script.sh
      artifacts:
        paths:
          - test_reports/
      only:
        - master

    deploy_job:
      stage: deploy
      script:
        - echo "Deploying application..."
        - deploy_script.sh
      only:
        - master
    ```

In this file, there are three stages defined: build, test, and deploy. Each stage has a job associated with it, and each job includes scripts to execute and conditions for when they should run.

The `.gitlab-ci.yml` file is a powerful tool in GitLab CI/CD, allowing you to automate the testing, building, and deployment of your applications seamlessly.

# Gitlab runner details

GitLab Runner is a crucial component in GitLab's Continuous Integration (CI) service. It is an application that works with GitLab CI/CD to run jobs in a pipeline. Here's a detailed explanation of its features, functionality, and usage:

### 1. **What is GitLab Runner?**
   - **Definition**: GitLab Runner is an open-source project that is used to run your CI/CD jobs and send the results back to GitLab. It's designed to run on the infrastructure you're already using, whether it's on a VM, a bare-metal machine, inside a Docker container, or on a Kubernetes cluster.
   - **Compatibility**: It's compatible with various operating systems and can be deployed in various environments.

### 2. **How GitLab Runner Works**
   - **Connection with GitLab**: The runner works by connecting to GitLab and asking for jobs. When a new job is available, GitLab sends the job's details to the runner, and the runner executes it.
   - **Execution Environment**: The runner executes each job in a separate environment. This can be a Docker container, a Kubernetes pod, a VM, a bare-metal machine, etc., depending on the runner's configuration.
   - **Isolation**: The use of Docker or Kubernetes as an executor provides strong isolation and reproducibility of the build environment.

### 3. **Types of Runners**
   - **Shared Runners**: Available to all groups and projects in a GitLab instance. Useful for jobs that have similar requirements, across different projects.
   - **Specific Runners**: Assigned to specific projects. They are useful when jobs have special requirements or when you need to ensure certain jobs run on certain machines.
   - **Group Runners**: Assigned to a group and all its projects. This is a midway point between shared and specific runners.

### 4. **Runner Executors**
   - Runners can use different executors to determine the environment each job runs in:
     - **Shell Executor**: Runs jobs in the system's shell. It's the simplest approach but offers the least isolation.
     - **Docker Executor**: Uses Docker containers to run jobs, offering good isolation and consistency.
     - **Docker Machine and Auto-Scaling**: For creating and managing dynamic environments with Docker.
     - **Kubernetes Executor**: Runs jobs in a Kubernetes cluster, offering great scalability and isolation.
     - **Virtual Machine (e.g., VirtualBox) and Parallels**: For running jobs in VMs.
     - **Custom Executors**: Advanced feature allowing you to define a custom environment.

### 5. **Installation and Configuration**
   - **Installation**: GitLab Runner can be installed on various platforms (Linux, macOS, Windows).
   - **Configuration**: After installation, it must be registered with a GitLab instance using a registration token. During registration, you specify details like the URL of the GitLab instance, the token, and the executor to use.

### 6. **Use Cases**
   - It's used for a variety of CI/CD tasks like running tests, deploying code, and building applications.
   - It can be used in development, staging, and production environments.

### 7. **Advantages**
   - **Flexibility**: Supports various languages and frameworks since it can run any script that can be executed in the runner environment.
   - **Scalability**: Particularly with Kubernetes or Docker Machine executors for dynamically handling the workload.
   - **Isolation**: Especially with container-based executors, ensuring that the CI/CD process is consistent and repeatable.

### 8. **Security**
   - Runners can be a security risk if not properly isolated and secured, as they have access to your codebase and might have access to deployment environments.

GitLab Runner is a powerful and flexible tool that extends the functionality of GitLab CI/CD. By understanding and properly configuring GitLab Runner, teams can automate their testing and deployment processes effectively, ensuring that their software is built, tested, and deployed consistently and efficiently.

# Create a Gitlab runner
Creating a new GitLab Runner involves several key steps. Here's a comprehensive guide to setting up a new Runner:

### 1. **Install GitLab Runner**
   - **Choose the Platform**: GitLab Runner can be installed on various platforms (Linux, Windows, macOS, Kubernetes).
   - **Download and Install**: Follow the [official installation instructions](https://docs.gitlab.com/runner/install/) for your specific platform. This typically involves downloading the binary and installing it on your system or deploying it in a Kubernetes cluster.

### 2. **Register the Runner**
   - **Get the Registration Token**:
     1. For a specific project: Go to your project in GitLab → Settings → CI/CD → Expand the Runners section. Here, you'll find the registration token.
     2. For a group: Go to your group's Settings → CI/CD → Expand the Runners section.
     3. For the whole GitLab instance (admin only): Go to the Admin area → Overview → Runners.
   - **Run the Registration Command**: On the machine where you installed the Runner, execute the `gitlab-runner register` command. This will prompt you for:
     - The GitLab instance URL.
     - The registration token you obtained earlier.
     - A description for the runner.
     - Tags associated with the runner (optional, but useful for organizing runners).
     - The executor (e.g., shell, docker, Kubernetes).
   - **Configure the Executor**: Depending on the executor you choose, you might need to provide additional configuration, such as the Docker image for the Docker executor.

### 3. **Verify Runner Setup**
   - After registration, the Runner should appear in the GitLab UI under the section where you got the token (project, group, or instance settings).
   - It should be listed as "active" and ready to pick up jobs.

### 4. **Configure the Runner's Behavior** (Optional)
   - **Edit `config.toml`**: The Runner's behavior can be fine-tuned by editing its `config.toml` file, located in the Runner's home directory. This includes configuring advanced features, caching, and more.
   - **Concurrency and Job Limits**: You can set up how many jobs the runner can handle concurrently.

### 5. **Secure the Runner** (Important)
   - If the Runner has access to sensitive data or production environments, ensure it's secured appropriately. Use a dedicated user for the Runner, and limit its access to what's necessary for CI/CD tasks.

### 6. **Start the Runner**
   - The Runner usually starts running automatically after installation and registration. If it's not running, use the appropriate system command to start the GitLab Runner service.

### 7. **Troubleshooting**
   - If the Runner isn't picking up jobs, check the Runner's logs for errors, ensure it's properly registered, and that there are no issues with network connectivity to the GitLab instance.

### 8. **Updating the Runner** (As Needed)
   - Keep the Runner updated to the latest version to ensure compatibility with GitLab and to receive the latest features and security updates.

Creating a GitLab Runner is a straightforward process, but it's important to carefully follow these steps and ensure that the Runner is configured securely, especially in a production environment. Properly set up, GitLab Runner is a powerful tool for automating your CI/CD pipeline.
