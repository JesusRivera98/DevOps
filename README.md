# DevOps
> DevOps = Developer Operations.

DevOps is trying to connect operators with developers in a more efficient way. Thus, the goals between both teams align, communication increases, and speed and results are higher.

DevOps is not a new person on the team or a new team.
DevOps is more ...:
|||
-|-
Culture| The change of culture in a company, the desire of both teams to collaborate.
Automation| Being able to reproduce infrastructure as well as bugs are reproduced. Generate a culture in which both developers and operators automate all their tasks.
Measurements| How much the goals of both teams take. Productivity is measured, how long a request to the API takes, how long it takes an operator to fix an incident in production, everything is measured.
Sharing| Better internal tools shared by both teams so that the code in production is always in high quality and can be fixed as quickly as possible.

With this, the idea is that one of the results is more deployments that contain fewer features and as a consequence, fewer errors in production.

### Docker File vs Docker Compose File
A docker file includes only commands to use the docker image while a docker compose file defines the services that are necessary to be able to run the application we are working on.



### How to use a Dockerfile and handle dependencies to have them locked in
One of the ways to solve the "" it works in my machine "" is by having homogeneity in all environments. Running code on our local machine should look as close to the test and production environment as possible.

Docker is recommended, it works for all operating systems (WIN10 Pro only) and it is reproducible, we can have an infrastructure that shares everything. The images are reproducible, programmable and the documentation is in the same code.
> Always install a version that you already used and tested.

-|-
-|-
FROM| I am looking for a source image and from there the container is mounted.
WORKDIR| It is recommended not to run all root. With this we tell Docker what our working folder is going to be.
ADD| It is where we indicate our dependencies as package.json, it caches that layer so as not to execute it every time we run our container. It also works for copying, as we do in the tenth line.
RUN| we tell docker to run a command. In this case npm install
EXPOSE| We expose port 3000
CMD| Here we tell Docker to execute this command when executing our container. In this case the application will run.
-|-
dockerignore| It is almost the same as gitignore, but for docker.


### Infrastructure as code
We can make infrastructure as code. Having the equivalent of docker in infrastructure, having the same configuration on different servers and regions, there are several options to do this and one of them is Terraform.

Terraform allows us to write ambiguous code that I can run on AWS in several regions and build the same infrastructure in all of them. We just have to pass the parameters and this will allow us to scale our applications

### Continuous Integration.

Before we enter Continuos Integration we must enter the fundamental part of CI and that is to do tests. Without evidence there is no confidence.

Our IC needs tests that must be run in an automated way such as unit tests, integration tests and acceptance tests, at least it is necessary to have the first two.

* Unit tests use mocks
* Integration tests use actual dependencies with fixtures
* Acceptance tests use a full-service environment, just like production.





With Git we make our changes in the code remain in a story that we can test before passing it to the master branch, knowing that our tests are passing successfully without breaking what we have in master.

Jenkins is our test automation, it downloads the latest version of our branch where a change was made and performs the tests we have and if they fail, it prevents us from breaking our main branch and tells us which tests failed to correct it.

We can also do a code analysis, we can have something very complex or a style that the team does not like and it can be changed in this part of the cycle and we keep the style guide good and clean code while we develop.

Artifacts is our unit that will pass to all environments, it must be something immutable. It's something we can store for a certain amount of time, maybe a year in case we need to rollback.

Integration tests are more productive, have more scope and have more value.

Something characteristic of CI is its implementation with various tools to strengthen the quality of our workflow. However, we must be very careful with this, as this process most likely works with access credentials to our production infrastructure, so, whenever possible, we always work with platforms that we can integrate within our infrastructure, and not that are externally hosted providers, because technically they would be storing credentials or keys on their servers with which to access our infrastructure.

### Continuos Delivery and Continuos Deployment
We have different ways of bringing our code to production. This Continuous Delivery and Continuous Deployment, also of course, we can do it by hand. The latter is not what we want.

The difference between Continuos Delivery and Continuos Deployment is quite simple, it is the same process, but in Continuos Deployment it is sent to production automatically based on the results of our acceptance tests and in Continuos Delivery we can do it by hand.

None is better than another, it all depends on what you are doing at the moment and the things you are taking to production. If it is something critical and there is no security, you can do it manually.

The final concept is to launch more frequent production and have fewer errors, the way implemented is a detail. The result should always be fewer errors.

There are several types of Deployments:

Name | Description
---- | -----------
Blue / Green| Have two tags of the same code updating one of them while the other serves the traffic.
Canary| This can be used in conjunction with other types. We have a pull of nodes and we are going to implement something new that could be risky. We only modify one of those nodes.
Rolling| It is updating machines one by one. They are safe as we can monitor progress.

### Acceptance tests
The acceptance tests must run in the staging environment and the production environment.

> *"Test all environments, at all times."*



### What to do when the phone rings:

* Measure the extent of the error (Measure the impact of the error).
* Communicate with the client and colleagues.
* Write a postmortem.



### Site Realiability Engineering
It is how companies internally measure that their products are doing well.

This allows us to measure our success. SLI: Serivece Level Indicators could be the amount of errors, latency, time to send an email, time to answer a specific path in our API. And the SLO: Service Level Objectives is the metric, that our latency is less than 50ms in a space of 5 minutes all month.

### Uptime

If we are going to measure our Uptime as an indicator of SLO and SLI you should use an external provider to have the internal and external metrics.

Both Pingdom and Ping tools set infrastructure around the world and then call the address that we tell them to check if we are available in each part. They also tell us how long it took to respond to our product or website.

### Logs

It is important to have structure in our logs to be able to parse. In this class we will see some examples of this type of structure logging. It is also important to make use of the Levels in the logs, both info, warning, error, fatal.

The Exception Trackers, an exception we know is an error that is not handled in our code and should have a special place to fix it as quickly as possible. There are several solutions for these types of problems, Sentry is recommended and allows us to send our exception to them and set rules. We can make our phone ring to fix it if it is something urgent.



Logs is when everything went wrong and I have no other way of knowing what happened.

That is why metrics help us to have a visualization, a dashboard of our services, being able to see our errors and make comparisons, see the frequency, peaks, latency, a call to the database.


### Common Commands
Command |	Description
------- | -----------
docker attach |	Attach local standard input, output, and error streams to a running container
docker build |	Build an image from a Dockerfile
docker builder |	Manage builds
docker checkpoint|	Manage checkpoints
docker commit|	Create a new image from a container’s changes
docker config|	Manage Docker configs
docker container|	Manage containers
docker context|	Manage contexts
docker cp|	Copy files/folders between a container and the local filesystem
docker create|	Create a new container
docker diff|	Inspect changes to files or directories on a container’s filesystem
docker events|	Get real time events from the server
docker exec|	Run a command in a running container
docker export|	Export a container’s filesystem as a tar archive
docker history|	Show the history of an image
docker image|	Manage images
docker images|	List images
docker import|	Import the contents from a tarball to create a filesystem image
docker info|	Display system-wide information
docker inspect|	Return low-level information on Docker objects
docker kill|	Kill one or more running containers
docker load|	Load an image from a tar archive or STDIN
docker login|	Log in to a Docker registry
docker logout|	Log out from a Docker registry
docker logs|	Fetch the logs of a container
docker manifest|	Manage Docker image manifests and manifest lists
docker network|	Manage networks
docker node|	Manage Swarm nodes
docker pause|	Pause all processes within one or more containers
docker plugin|	Manage plugins
docker port|	List port mappings or a specific mapping for the container
docker ps|	List containers
docker pull|	Pull an image or a repository from a registry
docker push|	Push an image or a repository to a registry
docker rename|	Rename a container
docker restart|	Restart one or more containers
docker rm|	Remove one or more containers
docker rmi|	Remove one or more images
docker run|	Run a command in a new container
docker save|	Save one or more images to a tar archive (streamed to STDOUT by default)
docker search|	Search the Docker Hub for images
docker secret|	Manage Docker secrets
docker service|	Manage services
docker stack|	Manage Docker stacks
docker start|	Start one or more stopped containers
docker stats|	Display a live stream of container(s) resource usage statistics
docker stop|	Stop one or more running containers
docker swarm|	Manage Swarm
docker system|	Manage Docker
docker tag|	Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
docker top|	Display the running processes of a container
docker trust|	Manage trust on Docker images
docker unpause|	Unpause all processes within one or more containers
docker update|	Update configuration of one or more containers
docker version|	Show the Docker version information
docker volume|	Manage volumes
docker wait|	Block until one or more containers stop, then print their exit codes

[Docker Documentation](https://docs.docker.com/engine/reference/commandline/docker/)
