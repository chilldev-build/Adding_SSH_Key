# SSH Creation and Using the SSH Agent from the command line

Feel free to fork this and add any details you learn from your system and testing this.

---

## Here are some notes for quick reference to create an SSH key from the command line.

github says to type the below in git BASH. When I attempted this it creaated the folder in C:\Users\chris instead of my Linux root. When I attempted to use the key I received an error.

$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

Instead of using Git BASH I attempted to use Ubuntu 18.04 BASH CLI and it created the folder here as needed: \\wsl$\Ubuntu-18.04\home\chilldev

After you run the command it will prompt you to Enter a file at the default location by pressing enter. This should work fine outside of the issue I had above using WSL 2 on windows.

We will have to test how this will work with WSL 1 windows users.

Next it will prompt you to add a passphrase.



<https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent>

---

## Once the key has been added you will need to manage the key in the agent to add to each directory.

Start the SSH agent:

$ eval $(ssh-agent -s)

You should see:
Agent PID xxxxx

xxxxx being the agent ID.

Then you add the key to the agent. I am not sure if you can do this at the top directory and if that will allow you to use it for any directory you add below.

So far I have added the key by starting the agent in a working directory and adding the key in that folder like so:

$ ssh-add ~/.ssh/id_rsa

#### Update

I ran these two commands in my Digital Crafts directory and then attempted to push a repo and it did not ask for the passphrase. Then I restarted my computer to see if the agent saves the setting and it appears to reset in this case.

After adding the key to the agent again at the root level I tested to see if restarting the terminal has any affect on the SSH Agent. This is that test.

It appears that restarting the terminal reset the SSH Agent as it promted me for my passphrase upon restarting the terminal and attempting to push to github.

I am not sure in all systems will behave this way or if there are some global settings where the key passphrase can be saved on a more permanent basis.

## Adding SSH Key to Github

https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account

You can copy your SSH key to the clip board with:

$ clip < ~/.ssh/id_rsa.pub

The above link describes the process to follow in Github.