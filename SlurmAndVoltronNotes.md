# Getting Started with Voltron (Aiden Lab’s Supercomputing Cluster)

Notes taken by: Michael Ngo  
Bulk of notes taken from Muhammad Shamim's video: [https://bcm.app.box.com/s/nrpjvqhd5joa8cefuhapw3v4e9wxpk68](https://bcm.app.box.com/s/nrpjvqhd5joa8cefuhapw3v4e9wxpk68)

## Accessing Voltron

- **to connect to VPN, click on the Cisco AnyConnect icon at top of screen → show AnyConnect window → enter [vpn.bcm.edu](http://vpn.bcm.edu) → enter credentials → when it asks for MFA security token, type “sms” and you’ll get a text for a 1-time use security token**
    - NOTE: this MFA security token must first be set up so that BCM knows what number to text the token to
        - link to install Cisco AnyConnect: [https://vpn.bcm.edu/+CSCOE+/logon.html#form_title_text](https://vpn.bcm.edu/+CSCOE+/logon.html#form_title_text)
        - link to set up MFA (multi-factor authentication) token: [https://bcm.service-now.com/bcmsp?id=kb_article&sys_id=c72f1a59db43cfc0729c73d78c961924](https://bcm.service-now.com/bcmsp?id=kb_article&sys_id=c72f1a59db43cfc0729c73d78c961924)
            - (recommend setting up ‘SMS text based token’
- **to use in terminal to access Voltron: ssh u123456@voltron.grid.bcm.edu** (but replace with actual BCM username)
- To end ssh session into voltron, just close terminal and reopen or use command ‘exit’

## Downloading Jars (or other files) into Voltron

- **wget** [jar/file url] is a command for CLI used to download a file from a url.
    - Before using, first download jars (or other files) into Dropbox or Box. **(For Rice students, I recommend we use Box** since we Rice gives us accounts with lots of storage) **then copy the link** for that file from Box or Dropbox and now finally we can use **wget [link]**
        - `wget https://rice.box.com/s/habyfolz6450c7krt4n358js88ehfok5`
        - another way to do this is to use cyberduck. http://voltron.grid.bcm.edu is the location. Instead of the command line, this is an interface more similar to Finder for Mac or File Explorer for Windows. You can just drag and drop into the proper folder within the Voltron machine
## Most Useful Slurm Commands

- Overall use of supercomputers:
    - Multiple clients can submit jobs for the supercomputer simultaneously. The scheduler assigns the jobs to particular compute nodes, ensures that as many jobs can be run at the same time as possible, that if one job crashes, the others won’t be affected, etc.
    - there are different types of scheduler softwares, the one we use is **slurm** workload manager
    - the main commands we use:
        - **squeue**
            - lists which users are currently running jobs/have jobs pending and on what node those jobs are on (you can determine whether or not there’s space to run your own job), and how long they’ve been running for
            - squeue -u [username] prints information on jobs being run by 1 specific user
            - **sqme**
                - only lists your current jobs
        - to submit a job, we must first provide the scheduler with information on it
            - **#!/bin/bash**
                - in practice, this line is called the ‘she-bang’. The she-bang at the head of the script tells the system that this file is a set of commands to be fed to the command interpreter indicated
            - **#SBATCH --job-name=** [jobName]
                - assigns a name to the job
            - #**SBATCH -o** [jobName]-%j.out
                - specifies output file. If we don’t specify a specific folder, it will automatically create the file in the working directory
                - note: it’s recommended to make a ‘debug’ directory in your work directory so that you don’t clog it up with these output and error files
                - the ‘%j’ can be considered as a variable representing the job ID. It’s good practice to include this in case you have multiple jobs with the same name and need to individuate
            - #**SBATCH -e** [jobName]-%j.err
                - specifies error file
            - **#SBATCH --mem-per-cpu=** [RAM in GB]
                - specifies RAM (for each cpu we’re using, giving it 10GB of RAM)
            - **#SBATCH --time=** [hours:minutes:seconds]
                - specifies time limit. At Rice, max time limit is 24 hr. In Voltron, you can do the command
                - note: you can also ignore the hours:minutes:seconds format and input a single number that will be interpreted as minutes
                - list a reasonable time for your job to take. This allows the scheduler to slot you in at an ideal time so that the max number of jobs can be completed. Longer times may not get fit into the schedule until later when there’s a bigger opening
                - Tip: use…
                    
                    **sinfo** to list available nodes, their time limits, and their state (e.g., down)
                    
            - #SBATCH --mail-user= [email]
                - (OPTIONAL) email you when you your job is done
            - #SBATCH --mail-type=\**ALL
                - (OPTIONAL) type of email
            - #SBATCH --dependency= [afterok:459:500:503]
                - (OPTIONAL) specify that this job won’t run until after some other jobs have been completed (specified by their job number). (useful if this job need results from other jobs)
                - note: I don’t exactly understand why afterok:459:500:503 was used as the example from the Youtube video I watched, but it was.
        - **sbatch [filename of Batch script -.sh]**
            - to submit batch job
- to google things such as default unit for these commands, look up “slurm sbatch [whatever command]”
- once you’ve written the commands you plan to use in a text editor (like Sublime) and save the file as “-.sh”, to copy the file here (into the your voltron account terminal), you can install Cyberduck, create the option for which we’ll SSH into the voltron server “SFTP (SSH File Transfer Protocol)”, insert info, drag and drop file into cyberduck
    - OR (the way I’ll be using), go directly through the terminal.
        
        in command line, type **vim [filename].sh** to create a new .sh file within the voltron account terminal. Press **i** for Insert mode, then copy-paste list of commands from Sublime into this Vim editor
        
- SSH (Secure Shell) is a network communication protocol that enables to computers to communicate and share data (compare this to http, or hypertext transfer protocol, which is the protocol used to transfer hypertext such as webpages)
- tip: use **cat** [filename] command in terminal to display contents of a file into command line interface
- a node, for our purposes, can be understood as a computer

- QUESTION: what is purpose of Cyberduck? You mentioned in the video that there are 2 options, you can drag and drop the files into Cyberduck or you can type the file directly into terminal. I saw that even when you did the second option by going through vim and everything, it still ended up in Cyberduck. What is Cyberduck doing and do you need it for the second option?
    - My Answer: Cyberduck seems really just like a file manager that you can use for the Voltron machine, allowing you to drag and drop files between your local computer (or DropBox folder, or Box) and folders within Voltron.
    - It’s perfectly fine to use Vim to create a new file from the proper directory when you’re ssh’ed into Voltron and then have that file contain your Batch script. Writing your Batch script into a local file and then drag-and-drop‘ing it into Voltron is just an alternative option

### Additional Notes on Slurm Taken from Outside Resources

- some of the potential states when you run **sinfo**:
    - alloc: allocated; maint: maintenance; drain: nodes that are not being used right now or cleaning up; **idle**: available
- sbatch is the command you use to launch batch scripts to be queued up for later work
    - **Batch Scripts** are stored in simple text files containing lines with commands that get executed in sequence. Automates command sequences in order to make one’s life at the shell easier and more productive
    - A shell script is a computer program designed to be run by the command-line interpreter
    - scripting languages do not require the compilation step and are rather interpreted (e.g., JavaScript does not need to be compiled)
- **scancel** [job number]
    - cancels job. Hard termination


