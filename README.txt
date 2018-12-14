This is a simple ansible-provisioned vagrant environment that runs under virtualbox on windows 10.
It may require adaptation for different environment, eat your cat or do something different and unpredictable.
If you're brave - let's get further.

To use this you will need:

1. Install virtualbox and vagrant (Download them from official site)

2. After installation is complete - open powershell and execute:
> vagrant plugin install vagrant-vbguest

3. Cd to directory where you cloned this repo.
Be sure that you have some disk space to download box for vagrant
and for virtual machine to whirl.

4. Edit file playbook.yml to fit it to your needs.

You don't need to dig in ansible for that, just correct some basic points and they are commented.

DO NOT USE TABS TO EDIT ANSIBLE PLAYBOOKS AND DON'T BREAK IDENTATION, OTHERWISE IT WOULDN'T WORK!

- Change your username (by default there would be created user with login 'user' and with password 'H@ngar51')
- Insert your public key for ssh. You can login as vagrant user though just with 'vagrant ssh' command, too.
- Edit minimal .gitconfig for user or comment this block of code whether you need git client to be preconfigured.

5. Edit Vagrantfile.
I hope that comments are more or less clear.

I use safe setup (internal virtualbox network, acessible from your host only).
Keep in mind all security concerns whether you would bring your machine to your network via bridging.
I prohibited root login via ssh (you can use L: root P: vagrant from VM's physical console as your last resort, though) and changed vagrant user password from default 'vagrant'.

Avoid intersections of IP addresses ranges with your existing networks. I tried to choose  failure-proof solution, but sh1t happens.

6. Run 'vagrant up' from powershell window in project's directory.
Magic starts and machine would be configured without your interaction. 
When it finishes, run 'vagrant ssh' to get onboard.

7. There's more.
You would be logged in as vagrant user. Run 'sudo -s' to escalate privileges.
After that 'su --login ansible'
Now, you are in /home/ansible, logged as user ansible and there are several playbooks.
I've configured inventory limited to localhost. You can use your own playbooks, modify inventory and make use of it the way you like.
For example, run 'ansible-playbook get-docker.yml' and it will perform simple installation of docker engine onboard and add users vagrant and user to docker group.
You will need to relogin and then you can play docker games all day long.


8. Some additional stuff to know.
You can shutdown VM by running:
- 'shutdown -h now' / 'init 0' # from ssh session
- from Virtualbox gui
- With powershell

cd to project's dir and run
vagrant status # to see if your setup is running
vagrant halt # to shutdown VM gracefully
vagrant reload # graceful reboot when changing vagrant settings, type of networking, etc.
vagrant destroy # to destroy this machine 
vagrant up # to rebuild this machine from scratch after destroy or turn it on.

There's a shared folder inside VM /vagrant.
It's shared with current project directory on host system, but keep in mind that it's not designed for heavy i/o because of vboxfs limited capabilities.
But it works quite well for sharing files.

