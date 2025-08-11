# Using Docker or Podman for Containerizing Code

We will containerize all packages which can be redistributed without licenses using Docker containers. You can work with these using either [Docker](https://www.docker.com/) or [Podman](https://podman.io/).

## Creating a New Dockerfile and Docker Image 

Create a local `Dockerfile` that loads/installs necessary packages (and their versions) necessary to run the code in the Github repo.

**How to create a docker registry in CAVATICA**

Create a repository

- Log into [CAVATICA](https://cavatica.sbgenomics.com/) using one of the lab accounts[^1]
- Click on `Developer` tab -> `Docker registry`
- Click `+ Create repository` (top right)
- Type repository name and choose visibility and click `create`.

![create-new-repo](img/Screenshot 2025-02-22 at 2.35.29PM.png)

- Assign admin rights to Jo Lynne Rokita (`harenzaj`) and Alex Sickler (`sicklera`) by clicking on: `<Name of Repository>/ Members`
- Assign admin rights to yourself so that you can push the image once it's built

**Docker Login**

From the directory where your Docekrfile lives, log into CAVATICA docker registry using your CAVATICA credentials. 

```bash
docker login http://pgc-images.sbgenomics.com/ -u <USERNAME> -p <YOUR-AUTH-TOKEN>
```

"USERNAME" refers to your CAVATICA username.
"YOUR-AUTH-TOKEN" can be generated from your CAVATICA account under the “Authentication token” section in the Developer tab.

**Build Image**

```bash
docker build -t pgc-images.sbgenomics.com/<username>/<repository_name>[:tag] .
```

*Example*: 
```bash
docker build -t pgc-images.sbgenomics.com/naqvia/autopvs1:latest .
```

For Mac users with Apple silicon chips (M1-M4 chip), you may need to specify the platform

```bash
docker build --platform=linux/amd64 -t pgc-images.sbgenomics.com/<username>/<repository_name>[:tag] .
```

*Example*: 

```bash
docker build --platform=linux/amd64 -t  pgc-images.sbgenomics.com/naqvia/autopvs1:latest .
```

**Push the Docker Image**

```bash
docker push pgc-images.sbgenomics.com/<username>/<repository_name>[:tag]
```

where `<username>/<repository_name>[:tag]` refers to the image that you have already committed

*Example*: `docker push pgc-images.sbgenomics.com/naqvia/autopvs1:latest`

## Pulling the Docker Image

```bash
docker pull pgc-images.sbgenomics.com/<username>/<repository_name>[:tag]:<tagname>
```

*Example*: 
```
docker pull pgc-images.sbgenomics.com/naqvia/autopvs1:latest
```

## Updating the Docker Image

Make any necessary changes to `Dockerfile` and run `docker build` as done previously. 

*Example*: 
```bash
docker build --platform=linux/amd64 -t pgc-images.sbgenomics.com/<username>/<repository_name>:latest .
```

Here, "username" should match the namespace used in the existing Docker container. For example, it should be "rokita-lab", not your personal CAVATICA username, in the repository below.

```bash
docker pull pgc-images.sbgenomics.com/rokita-lab/haydar-mirna:v1.0.1
```

Once complete, the output will print `Successfully built <image ID>`. Tag this image ID to the remote repo and push using these steps: 

```bash
docker tag <image ID> pgc-images.sbgenomics.com/<username>/<repository_name>:[tag]
docker push pgc-images.sbgenomics.com/<username>/<repository_name>:[tag]
```

For more, please review the [full documentation](https://docs.sevenbridges.com/docs/manage-docker-repositories-advance-access).

For more about Docker using M1/M2/M3 chip macs, ([see here](https://tutorials.tinkink.net/en/mac/how-to-use-docker-on-m1-mac.html)).

[^1]: CAVATICA logins for Children's BTI and Rokita Lab are pinned to #rokita-lab-internal slack channel.
