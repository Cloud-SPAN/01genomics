---
title: "Logging onto the Cloud"
teaching: 5
exercises: 40
questions:
- How do I connect to an AWS instance?
objectives:
- Log onto to a running instance
- Log off from a running instance
keypoints:
- You can use one set of log-in credentials for many instances
- Logging off an instance is not the same as turning off an instance
---

<script language="javascript" type="text/javascript">
function set_page_view_defaults() {
    document.getElementById('div_aws_win').style.display = 'block';
    document.getElementById('div_aws_unix').style.display = 'none';
};

function change_content_by_platform(form_control){
    if (!form_control || document.getElementById(form_control).value == 'aws_win') {
        set_page_view_defaults();
    } else if (document.getElementById(form_control).value == 'aws_unix') {
        document.getElementById('div_aws_win').style.display = 'none';
        document.getElementById('div_aws_unix').style.display = 'block';
        document.getElementById('div_hpc').style.display = 'none';
        document.getElementById('div_cyverse').style.display = 'none';
    } else {
        alert("Error: Missing platform value for 'change_content_by_platform()' script!");
    }
}

window.onload = set_page_view_defaults;
</script>

## Important Note

This lesson covers how to log into, and out of, an *already running* Amazon instance.

## Background to AWS

An Amazon Web Services (AWS) instance is a **remote computer** that runs on AWS infrastructure and that is accessible from any laptop or desktop as described below. Setting up a new AWS instance requires a credit card, an AWS account, and up to a day of verification time. 

To save time, your instructor has launched an AWS instance for you prior to the course, and connected it to our lesson data and software analysis tools. It all works as follows.

We have a pre-configured copy of the data and software analysis tools needed for this course that is always available to attach to a new AWS instance that is accessible to you as long as you have the log-in credentials to open it.

To login into your AWS instance for this course, you'll need:
- the name of your instance and a login key file, both of which you received via email
- the shell/terminal application --- **Windows users** should have already installed the *Git Bash* shell; otherwise follow the directions in the [Setup](../setup)
- the *secure shell* (**ssh**) application, which is readily available in MacOS, Linux and Windows. **Windows users** will use ssh through Git Bash. 

As the name implies, **ssh** provides you with a secure (encrypted) way to use a remote *shell*, as simple as this (you do not have to type this yet):

 ~~~
 $ ssh -i login-key-instanceNN.pem  csuser@instanceNN-gc.cloud-span.aws.york.ac.uk
 ~~~
 {: .bash}

A few seconds after you enter that command to the shell in your computer, you will be logged into your AWS instance and start using a (Linux) shell running in your instance.


## Create a folder for the course
To keep things tidy and easily accessible, create a folder (or directory) to keep everything related to this course: your login key file, your notes, data, etc. If you have completed the Prenomics course, you will have already made a `cloudspan` folder. If that is the case, you can ignore the next couple of sets of instructions and instead navigate to your existing folder.

## Create a folder for the course

In theory you can make your Cloud-SPAN directory anywhere in your file system but we recommend making it inside your Desktop folder, to make it easy to access.

1. **Create the folder** `cloudspan` in your *Desktop*.

   Minimise all windows until you can see your desktop background. Right click and select *New*, then *Folder*. Name the folder `cloudspan`.

   You should see a folder icon appear on your desktop with the label `cloudspan`.

   Additionally, if you enter your file explorer application you should be able to click on the *Desktop* directory at the side and see the `cloudspan` folder.

2. **Write down the absolute path** to your `cloudspan` folder.

   Find out what the absolute path is using your file manager application. Right click on the folder, or in any blank space inside the folder, and select *Properties*.

   The field called *Location* will tell you the absolute path for your folder. Once you have this written down, do not lose it! Now you can find your way back to the `cloudspan` folder whenever you need to, no matter where you are in your file structure.

## Download your login key file

Next we will download your unique login key file from the email you received from the Cloud-SPAN team. This type of file is called a `.pem` file. It contains a certificate which allows you to communicate with the Cloud securely. Without the `.pem` file you cannot access the Cloud.

For now we will use the file explorer to move the `.pem` file around.

1. **Find out where downloads are saved** on your computer.

   How you so this will depend on which browser you use. You can find instructions for changing your default download location in [Chrome](https://support.google.com/chrome/answer/95759?hl=en-GB&co=GENIE.Platform%3DDesktop), [Edge](https://support.microsoft.com/en-us/microsoft-edge/find-where-your-browser-is-saving-downloads-d3e83af6-68bb-aa90-3167-eeb657013902) or [Safari](https://support.apple.com/en-gb/guide/safari/sfri40598/mac).

   If you already know which folder your downloads go to, then you can skip this step.

2. **Download your login key file** to the folder you just created.

   Click on the link embedded in the email you received from the Cloud-SPAN team.
   
   **Mac users** may need to Click on 'download' when the file says it can't be opened.

   If your browser asks you "where do you want to download the file?", choose the `cloudspan` directory.

   Otherwise, once downloading is finished, copy and paste/drag and drop your login key file from wherever it was downloaded to your `cloudspan` folder.

If you were skipping the steps above having already made your `cloudspan` folder, here is where you shoud pay attention again.

## Login into your instance with ssh

1. Copy and paste the command in the Code box below to your *terminal*, but **replace** `NN` with the number in your login key file name.

    Windows Git Bash users only:
    - **copy** the command the usual Windows way: (1) highlight it with the mouse pointer while pressing the mouse left button and (2) press Ctrl-v (keys Ctrl and v simultaneously).
    - but **paste** it the Linux/Unix way: by pressing the mouse middle button while hovering the mouse pointer over the Git Bash window. (Try with the right button if the middle button doesn't work.)

    ~~~
    $ ssh -i login-key-instanceNN.pem  csuser@instanceNN-gc.cloud-span.aws.york.ac.uk
    ~~~
    {: .bash}

    *Be sure to replace* `NN` *twice.* You can use the left and right arrow keys to move to where NN is.

    The `-i` option tells `ssh` the identity file containing the key to send to your AWS instance for it to check that you have access permissions to connect as an *ssh client*. 

    **NB**: `ssh` looks for the identity file in the directory where you are, Desktop/cloudspan (that you moved to with the command `cd` above), which is the same directory wherein you downloaded your login key file.  


2. The terminal will display a security message, after you enter the `ssh` command, *similar* to the one below: 

    ~~~
    The authenticity of host 'instance06-gc-cloud-span.aws.york.ac.uk (52.211.132.120)' can't be established.ECDSA key fingerprint is SHA256:8N054prkkCeM4GCDSsa0AUnSQw5ngBQHbOR40FqfqLg.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? 
    ~~~
    {: .output}

    Type **yes** to continue and get connected to your AWS instance.

    The terminal will display a few messages and at the end the **prompt** of the **shell running** on your Linux AWS instance:

    ~~~
    ...
    csuser@instance05-gc:~ $
    ~~~
    {: .output}

    Note that you did not need to give a password to login to your instance --- you are using your login-key file for authentication.

## Logging off your cloud instance

Logging off your instance is a lot like logging out of your local computer but it doesn't shut the computer off. **Be aware that AWS instances accrue charges whenever they are running, even if you are logged off**. Today, however, you do not need to worry about this!

To log off, use the `exit` command in the same terminal you connected with. This will close the connection, and your terminal will go back to showing your local computer prompt, for example:

~~~
csuser@instance05-gc:~ $ exit
~~~
{: .bash}
~~~
logout
Connection to instance05-gc.cloud-span.aws.york.ac.uk closed.
Amanda-MacBook-Pro-3 $
~~~
{: .output}

## Subsequent logins to your AWS instance

To login back to your instance, open a terminal, move to the directory you created for the course, and `ssh` as before:

~~~ 
$ cd Desktop/cloudspan
$ ssh -i login-key-instanceNN.pem  csuser@instanceNN-gc.cloud-span.aws.york.ac.uk
~~~
{: .bash}
