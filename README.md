## Setup Local Env for GC Development using Docker
1. Open Docker Desktop, and build a new container with an ubuntu image
    ```
    sudo docker pull ubuntu
    sudo docker run -ti ubuntu /bin/bash
    ```
2. Install Google Chrome and ChromeDriver
    - dependencies:
         ```
         apt-get update
         ```
         ```
         apt-get install -y curl unzip xvfb libxi6 libgconf-2-4
         ```
         ```
         apt-get install wget
         ```
         ```
         apt-get install sudo
         ```
         ```
         apt-get install unzip
         ```
         ```
         apt-get install -y git
         ```
     - download Chrome first:
       ```
          wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb --no-check-certificate
       ```
       ```
         sudo apt install ./google-chrome-stable_current_amd64.deb
       ```
       ```
         google-chrome --version
       ```
     - download Chromedriver
         - references: https://www.gregbrisebois.com/posts/chromedriver-in-wsl2/, https://tecadmin.net/setup-selenium-chromedriver-on-ubuntu/
       ```
        wget https://edgedl.me.gvt1.com/edgedl/chrome/chrome-for-testing/120.0.6099.109/linux64/chromedriver-linux64.zip --no-check-certificate
        unzip chromedriver-linux64.zip 
        sudo mv /path/to/chromedriver /usr/local/bin
       ```
         - tip: to find path
             ```
               find $(pwd) -name chromedriver
             ```
    - after a successful installation you should be able to run the following from the shell:
         ```shell
         chromedriver --version
         ```
3. Install Miniconda or Anaconda (Miniconda is much smaller)
    - https://docs.conda.io/en/latest/miniconda.html
    - https://www.jamesbower.com/how-to-install-conda-and-miniconda3-on-ubuntu-22-04-lts/
      ```
        wget https://repo.anaconda.com/miniconda/Miniconda3-py310_22.11.1-1-Linux-x86_64.sh
        bash Miniconda3-py310_22.11.1-1-Linux-x86_64.sh -b -p /opt/miniconda
        rm Miniconda3-py310_22.11.1-1-Linux-x86_64.sh
        export PATH="/opt/miniconda/bin:$PATH"
      ```
    - after a successful installation you should be able to run the following from the shell:
         ```shell
         conda --version
         ```
4. Create a gamechanger crawlers python3.6 environment:
     ```shell
     conda create -n gc-crawlers python=3.6
     ```
5. Clone the repo and change into that dir:
     ```shell
     git clone https://github.com/dod-advana/gamechanger-crawlers.git
     cd gamechanger-crawlers
     ```
6. Configure shell
   ```
   conda init bash
   ```
7. You will need to restart your container
   - exit container
   - if it shut down, restart it
    ```
    sudo docker start <CONTAINER_NAME>
    docker exec -it <CONTAINER_NAME> bash
    ```
8. Activate the conda environment and install requirements:
     ```shell
     conda activate gc-crawlers
     cd gamechanger-crawlers
     pip install --upgrade pip setuptools wheel
     pip install -r ./docker/core/minimal-requirements.txt
     ```
9. If you have VSCode, you can attach to your Docker container through there to edit scripts
10. If you cannot run scripts through the terminal within VSCode, then use an Ubuntu terminal
