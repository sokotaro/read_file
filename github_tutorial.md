# GitHub Intro Tutorial
![Github icon](http://code-bude.net/wp-content/uploads/2013/10/1372714624_github_circle_black.png)


1. [Git Installation](#install)
2. [Setup GitHub](#setup)
3. [Setup Collaborators](#collaborate)
4. [Updating GitHub Project](#update)
5. [Git Cheat Sheet](http://rogerdudler.github.io/git-guide/files/git_cheat_sheet.pdf)
6. [Awesome Git Guide](http://rogerdudler.github.io/git-guide/)

## <a id="install"></a> 1. Git Installation

#### Windows
Git Download:    [|32-bit|](https://github.com/git-for-windows/git/releases/download/v2.10.0.windows.1/Git-2.10.0-32-bit.exe) 
[|64-bit|](https://github.com/git-for-windows/git/releases/download/v2.10.0.windows.1/Git-2.10.0-64-bit.exe)

#### Linux
Open Terminal and run the command for your distro

>**Debian/Ubuntu**  
>```bash
>sudo apt-get install git-all
>```

>**Fedora**  
>```bash
>sudo yum install git (up to Fedora 21)
>sudo dnf install git (Fedora 22 and later)
>```

>**Arch Linux**  
>```bash
>sudo pacman -Syu git
>```

#### Mac
Open Terminal and run the following three commands

1.	Install Command Line Tools for Xcode

	>```bash
	>xcode-select --install
	>```
2. Install Homebrew "<http://brew.sh>"

	>```bash
	>/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
	>```
3. Install Git

	>```bash
	> brew install git
	>```


--

## <a id="setup"></a> 2. Setup GitHub (master)
*This step will create the (master) GitHub project.  Collaborators can be added to make changes/updates.*

#### Create a GitHub Account
>Navigate to the [GitHub homepage](https://github.com), fill out the form, and click the "Sign up for GitHub" button
>You will receive an email with a verification link.  Click on that link to verify your email.

#### Start a New Project
>Click on the "Start a New Project button" type in a **Repository Name** and click the **Create repository** button
>For this tutorial, I will create a repository called *read_file*
>![img](https://github.com/kkatayama/test_project/blob/master/create_repo_2.png?raw=true)

#### Add Collaborators
>Once you have created a new repository, click on the Settings tab and click on **Collaborators**.

>Then type each user you wish to add and click on **Add collaborators**
>![img](https://github.com/kkatayama/test_project/blob/master/add_collab.png?raw=true)
>Each user you add will receive an email containing an invitation link to your GitHub repo.<br />
>Once they click on the link, that user will be able to upload changes.

#### Add, Commit, and Push Files
>At this point, you should have Git installed and an empty repo on your GitHub account. <br />
>Now let's write some code and add files to your empty repo.<br />
>Open Terminal and create a directory and **cd** into that directory.<br />
>Because my repo is called "read_file", I will create a directory called "read_file".
>```bash
>$ mkdir read_file
>$ cd read_file
>```
>Now let's add some files to this directory.<br />
>For this example, I will add two files: read_file.cpp & test_file.txt<br />
>read_file.cpp reads in a text file, prints out its contents, and saves it to output.txt.<br />
>test_file.txt is a sample text file to read in.<br />
>##### read_file.cpp
>```c++
>#include <fstream>
>#include <iostream>
>#include <sstream>
>
>using namespace std;
>
>int main (int argc, char *argv[]) {
>  if (argc !=2) {
>    cout << "usage: " << argv[0] << " <filename>\n";
>  } else {
>    ifstream the_file(argv[1]);
>
>    if (!the_file.is_open()) {
>      cout << "Could not open file\n";
>    } else {
>      string text;
>      stringstream buffer;

>      /* Read a text file */
>      buffer << the_file.rdbuf();
>      text = buffer.str();

>      /* Print out the contents of the file */
>      cout << text;

>      /* Save string to file */
>      ofstream out("output.txt");
>      out << text;
>      out.close();
>    }
>  }

>  return 0;
>}
>```
>##### test_file.txt
>```text
>This is a test to read in the contents of this file, print it out, and save it to output.txt
>
>Hopefully this works!!!
>```
>If you want to compile and run this test code:
>```bash
>$ g++ read_file.cpp -o read_file
>$ ./read_file test_file.txt
>```
>Once you have added your files to your local directory, let's add them to the GitHub repository.<br />
>**Since this is the first time to add anything to your repo, you have to run the following command:**
>```bash
>$ git init
>```
>which should ouput something similar to this:
>```bash
> Initialized empty Git repository in /Users/tekataya/Documents/read_file/.git/
>```
>Now let's add the files we wish to commit to our repo.
>```bash
>$ git add read_file.cpp test_file.txt
>```
>Add a commit message.
>```bash
>$ git commit -m "First Commit"
>```
>which should output something similar to this:
>```bash
>[master (root-commit) 15b096d] First commit
> 2 files changed, 38 insertions(+)
> create mode 100644 read_file.cpp
> create mode 100644 test_file.txt
>```
>Since this is the first commit to our GitHub repo, we need to add the origin.<br />
>In this example, my username is **sokotaro** and my git file is my folder name + git **read_file.git**<br />
>So the command I would run would look like this:
>```bash
>$ git remote add origin https://github.com/sokotaro/read_file.git
>```

#### Push Changes
>Before we push changes, let's define our authentication information and cache it<br />
>Run the following commands with your user_name and email_address:
>```bash
>$ git config --global user.name "sokotaro"
>$ git config --global user.email "sokotaro3@gmail.com"
>```
>Now let's cache our credentials.  This command will vary based on your operating system<br />
>>##### Windows
>>```bash
>>$ git config --global credential.helper wincred
>>```
>##### Linux
>```bash
>$ git config --global credential.helper cache
>$ git config --global credential.helper 'cache --timeout=3600'
>```
>##### Mac
>```bash
>$ git config --global credential.helper osxkeychain
>```

>Finally let's push the files into our GitHub repository
>```bash
>$ git push -u origin master
>```
>If successful, you should see an output like the following:
>```bash
>Counting objects: 4, done.
>Delta compression using up to 8 threads.
>Compressing objects: 100% (4/4), done.
>Writing objects: 100% (4/4), 662 bytes | 0 bytes/s, done.
>Total 4 (delta 0), reused 0 (delta 0)
>To https://github.com/sokotaro/read_file.git
> * [new branch]      master -> master
>Branch master set up to track remote branch master from origin.
>```

--
## <a id="collaborate"></a> 3. Set up Collaborators
*This step is for the collaborators who wish to make their first update/changes to an existing (master) repository*

#### Clone a Repository
>Since this is the first time we are making changes to the master repository, we need to obtain a local copy.<br />
>In this example, the (master) repo I created in Step 2 is called **read_file** and the user_name is **sokotaro** <br />
>The following commands will make a local copy of the **read_file** repo and change into that directory:
>```bash
>$ git clone https://github.com/sokotaro/read_file
>$ cd read_file
>```
>If successful, you should see an output similar to this:
>```bash
>Cloning into 'read_file'...
>remote: Counting objects: 4, done.
>remote: Compressing objects: 100% (4/4), done.
>remote: Total 4 (delta 0), reused 4 (delta 0), pack-reused 0
>Unpacking objects: 100% (4/4), done.
>Checking connectivity... done.
>```

#### Make Changes to Repository
>At this point, you now have a local copy of the repo.  Let's make a change such as adding a readme file.<br />
>Create a file called **README.md** and add some text.
>##### README.md
>```
>test read me file
>```
>Now add the **README.md** file to be pushed into the GitHub repo.
>```bash
>git add README.md
>```
>Add a commit message.
>```bash
>git commit -m "Added a README.md file"
>```
>which should output something similar to this:
>```bash
>[master 6b92429] Added a README.md file
>1 file changed, 1 insertion(+)
>create mode 100644 README.md
>```
>Since this is the first time we are making changes to the GitHub repo, we need to add the origin.<br />
>In this example, the (master)username is **sokotaro** and the folder name + git is **read_file.git**<br />
>So the command I would run would look like this:
>```bash
>$ git remote add origin https://github.com/sokotaro/read_file.git
>```

#### Push Changes
>Before we push changes, let's define our authentication information and cache it<br />
>Run the following commands with your user_name and email_address:
>```bash
>$ git config --global user.name "kkatayama"
>$ git config --global user.email "katayama@udel.edu"
>```
>Now let's cache our credentials.  This command will vary based on your operating system<br />
>>#####Windows
>>```bash
>>$ git config --global credential.helper wincred
>>```
>#####Linux
>```bash
>$ git config --global credential.helper cache
>$ git config --global credential.helper 'cache --timeout=3600'
>```
>#####Mac
>```bash
>$ git config --global credential.helper osxkeychain
>```

>Finally let's push the files into our GitHub repository
>```bash
>$ git push -u origin master
>```
>If successful, you should see an output like the following:
>```bash
>Counting objects: 3, done.
>Delta compression using up to 8 threads.
>Compressing objects: 100% (2/2), done.
>Writing objects: 100% (3/3), 339 bytes | 0 bytes/s, done.
>Total 3 (delta 0), reused 0 (delta 0)
>To https://github.com/sokotaro/read_file
>   15b096d..6b92429  master -> master
>```


## <a id="update"></a> 4. Updating GitHub Project

##### Synchronize With Latest Version
>Before you make any changes to any file, it is important that you are working with the latest copy.
>Open the folder that contains the local copy of the GitHub repository and run the following command:
>```bash
>$ git pull
>```
>This will update your local files with the latest versions

#### Add & Commit Files
>Make changes to the files you wish to update. <br />
>In this example, I will edit the **README.md** file that a collaborator had added in step 3.

>>#####Old README.md
>>```
>>test read me file
>>```
>##### New README.md
>```
>Read File Program
>```

>Now add the changed **README.md** file to be pushed into the repo.
>```bash
>$ git add README.md
>```

>Include a commit message
>```bash
>$ git commit -m "Update the README.md file"
>```
>If succesful, you will see an output like the following:
>```bash
>[master e92927c] Update the README.md file
> 1 file changed, 1 insertion(+), 1 deletion(-)
>```

#### Push Changes
>Now we are ready to push the changes.
>```bash
>$ git push origin master
>```
>If successful, you will see an output similar to the following:
>```bash
>Counting objects: 3, done.
>Delta compression using up to 8 threads.
>Compressing objects: 100% (2/2), done.
>Writing objects: 100% (3/3), 341 bytes | 0 bytes/s, done.
>Total 3 (delta 0), reused 0 (delta 0)
>To https://github.com/sokotaro/read_file
>   6b92429..e92927c  master -> master
>```

#### GUI View of the Project
>To see a GUI view of the project, either run the following command or access the repo online via github.com
>```bash
>$ gitk
>```
>![img](https://github.com/kkatayama/project1/blob/master/gitk.png?raw=true)

>[https://github.com/sokotaro/read_file](https://github.com/sokotaro/read_file)
>![img](https://github.com/kkatayama/project1/blob/master/web.png?raw=true)

