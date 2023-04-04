# Accessing repositories

The repositories pertainig to this project are all under the github organization. See [here](../introduction.md#github) for relevant links.

The process for accessing and contributong to these repositories is very straightforward. 

1. Go to the repository you wish to contribute to.
2. Copy the repository link
    ![image](https://i.imgur.com/8YffvCV.png)

3. In your terminal, execute 
    ```bash
    git clone <repo_url>
    cd <repo_name>
    ```

As an example, let's clone the repository that holds the markdown files for this website:

1. Get the url from [GitHub](https://github.com/Cool-Corridors/cool-corridors.github.io). Use the above image for assistance.

2. Enter a terminal and git clone. 
    ```bash
    git clone https://github.com/Cool-Corridors/cool-corridors.github.io.git
    cd cool-corridors.github.io
    ```

You can now make whatever changes you want and then commit back to this repository. Best practice is to create a branch for new features, and then merge them back into the main branch through a pull request. For more information about git, check out their [docs](https://git-scm.com/docs) or just google it.  

