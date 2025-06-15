# Using GitHub

For general information on using GitHub, [see here](https://git-scm.com/doc).

## Setting up a local SSH Key and adding to GitHub

On your local computer (or EC2 instance for the first time), run the following command to generate your public SSH key.

```bash
ssh-keygen
<enter>
<enter>
<enter>

cat ~/.ssh/id_rsa.pub
```

Add this new SSH key to your profile in GitHub by following [these instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).


## Setting up a GitHub repository

1. **Clone remote GitHub repo onto local computer using SSH:**
    
        git clone git@github.com:rokitalab/OpenPedCan-Project-CNH.git

2. **Obtain latest version of project Docker image using Docker or Podman:**

        docker pull pgc-images.sbgenomics.com/rokita-lab/openpedcanverse:latest
        podman pull pgc-images.sbgenomics.com/rokita-lab/openpedcanverse:latest

3. **Run the Docker container**
    
    **For Local Development**:
        
          docker run --name <CONTAINER_NAME> --platform linux/amd64 -d -e PASSWORD=pass -p 8787:8787 -v $PWD:/home/rstudio/OpenPedCan-Project-CNH pgc-images.sbgenomics.com/rokita-lab/openpedcanverse:latest

      Alternatively, the container can be initialized through the Docker dashboard on desktop.
        
      Mac and Linux users can also run Rstudio in the project docker container from a web browser. After executing the above `docker run` command, navigate to `localhost:8787` in your web browser. The username for login is `rstudio` and the password will be whatever password is set in the `docker run` command above (default: `pass`)
        
    **For development using Amazon EC2**:
          
          docker run --platform linux/amd64 --name <CONTAINER_NAME> -d -e PASSWORD=pass -p 80:8787 -v $PWD:/home/rstudio/OpenPedCan-Project-CNH pgc-images.sbgenomics.com/rokita-lab/openpedcanverse:latest

      To launch RStudio in a browser, enter the IP address in a web browser. The username for login is `rstudio` and the password is `pass` (default) or whatever was specified in the `docker run` command.  

4. (Optional) Once running, a bash shell can be opened into the container to run analyses. For example if `<CONTAINER NAME>` = openpedcan, run the following command from the root directory: 
        
          docker exec -ti openpedcan bash
        
      From here, you can navigate to the module of interest as follows: 
        
          cd /home/rstudio/OpenPedCan-Project-CNH/analyses/module-of-interest
        
5. **Download project data**
    
    Data can typically be downloaded via a [download-data.sh](http://download-data.sh) shell script in the project root directory: 
    
        bash download-data.sh
    
    This will download all project data from the associated Amazon S3 bucket and create symlinks in `data/` to the latest data release version. This command can be re-run to ensure that the most updated files are downloaded. 
    

## Data release instructions

For generating a new versioned data release, follow the steps below:

1. **Create a versioned folder in S3**

    Create the new version folder in the designated S3 bucket:

        s3://<bucket-name>/<repo-name>/v1/

    Upload all finalized data files for this release into the versioned folder.

2. **Generate MD5 checksums for uploaded files**

    Run the following command from your local machine where the data files are stored:

        md5sum * > md5sum.txt

    Upload the md5sum.txt file to the same S3 folder.

        aws s3 cp md5sum.txt s3://<bucket-name>/<repo-name>/v1/

3. **Verify file uploads**
    (Optional, but recommended)

        aws s3 cp s3://<bucket-name>/<repo-name>/v1/md5sum.txt .
        md5sum -c md5sum.txt

4. **Update download_data.sh in the GitHub repository**

    Pull the latest version of the repository locally:

        git pull origin main
    
    Edit download_data.sh to add the newly released version folder. For example, for version v1:
    
        RELEASE=${RELEASE:-v1}

    Test the updated download script locally to ensure correct download of files:

        bash download_data.sh
        cd data/v1
        md5sum -c md5sum.txt

    Commit and push your changes:

        git add download_data.sh
        git commit -m "Add v1 data release to download_data.sh"
        git push origin <branch-name>

    Open a Pull Request with a description of the data release changes.


## Creating submodules

The following is a good resource: [https://git-scm.com/book/en/v2/Git-Tools-Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

Below is documentation from Kelsey Keith at CHOP:

```markdown
## Git Submodules

Followed the instructions in the git book for setting up a submodule, <https://git-scm.com/book/en/v2/Git-Tools-Submodules>

### Toy Example of How to Set up a Submodule
*2022-09-02*

Setting up a repo as a submodule of another repo. 
I used two personal private toy repositories `practice` and `old_practice_repository`

```bash
git clone https://github.com/kelseykeith/practice.git
cd practice
git submodule add https://github.com/kelseykeith/old_practice_repository
git submodule init
git submodule update
```

Go to the other repository, make some changes, and then you can sync them into the other repository it's a submodule of

```bash
git clone https://github.com/kelseykeith/old_practice_repository
cd old_practice_repository
echo 'submodule testing' > submodule_test.txt
git add submodule_test.txt 
git commit -m 'using this repo and the practice repository repo to practice adding a git submodule'
git push
cd /path/to/practice/repository
git submodule update --remote --merge
```
Setting up `OpenPedCan-analysis` as a submodule of `documentation` so that I can reference `OpenPedCan-analysis` files

```bash
cd documentation
git checkout main
git checkout -b table-update
git submodule add https://github.com/PediatricOpenTargets/OpenPedCan-analysis.git
# reset submodule to the last v10/v1.0.0 commit
git reset --hard c0e5692e2949ad30b8e087ff0ec4e9385bde4b13
```
