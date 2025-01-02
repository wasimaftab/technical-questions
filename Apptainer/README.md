# Singularity/Apptainer Questions

## Question 1
- What is Singularity/Apptainer, and how does it differ from Docker?
- The term Singularity and Apptainer is used interchangeably. But what is the difference between the two?
- Why is it commonly used in High-Performance Computing (HPC) environments?


## Question 2
Explain what the following Singularity commands do:

- `singularity exec my_image.sif ls /`
- `singularity shell --bind /data:/mnt my_image.sif`

## Question 3
You need to create a Singularity container for an application that requires specific system libraries. How would you use a definition file (`.def`) to do this?
What are the purposes of the following sections in a definition file:

1. `%post`
2. `%environment`
3. `%runscript`


## Question 4
Predict what happens when you execute this command:

```bash
singularity exec --bind /data:/mnt my_image.sif ls /mnt
```
- What does the `--bind` flag do?
- What will the output show if `/data` exists on the host, and if it doesn't exist?

## Question 5
Describe how Singularity ensures security compared to Docker when running containers.

- What is the importance of running containers as a non-root user?
- How does Singularity handle permissions differently than Docker?


## Question 6
A colleague wants to use a Docker image available on DockerHub but is restricted to Singularity on an HPC system.

- How can they convert the Docker image into a Singularity container?
- What are potential issues they might face in this process as a non-root user?
- Can you create a Docker image using a Singularity container?


## Question 7
A colleague runs the following command on an HPC cluster:

```bash
singularity run my_pipeline.sif
```

However, they find that it fails because some necessary input files are not accessible.

What could be the issue? How can they fix it using Singularity's options?


## Question 9
- What is the difference between a sandbox image and a regular image?
- How do you build a sandbox image?

## Question 10
You run this command on an HPC system:

```bash
singularity exec --bind /scratch:/data my_image.sif python script.py
```
However, the script fails because a Python library is missing.

- How can you include the necessary Python library in the Singularity image?
- If modifying the image is not allowed, what alternative solutions could you use?

## Question 11
Singularity allows users to define environment variables within a container using the `%environment` section in a definition file.

- What is the difference between defining an environment variable in `%environment` and `%post`?
- When would you use one over the other?


## Question 12
You are given a base `.sif` image called `base_image.sif`, and you need to install the latest version of Python to it.

- Can you modify the image directly? Why or why not?
- Describe how you would customise the local image that is reproducible.
- What section of the definition file would you use to install the latest version of Python, and what commands might you include?


## Question 13
You created a Singularity container and you want to make it publicly available so that others can pull it (e.g. your collaborators).

- What options do you have to distribute your container?


## Question 14
Your colleague runs a Python script inside a Singularity container using the following command:

```bash
singularity exec my_container.sif python3 script.py
```

However, an error is raised because the container is using a Python library from your colleague's home directory instead of the version installed in the container. 

- Why is the container defaulting to the library in the colleague's home directory?
- How can you confirm which library version Python is using during execution?
- Suggest a simple fix for the colleague to resolve this issue