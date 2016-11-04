Steps to set up the build environment:

1. Clone Vagrant from the Alion GitHub: https://github.com/AlionScience
2. Run Windows PowerShell as Administrator.
3. Navigate to the local vagrant directory and type "vagrant up". Wait for the command prompt
   to return before proceeding to the next step.
4. A VirtualBox window will appear running Ubuntu.  Login with user/password: vagrant/vagrant
5. Open a terminal window and type "eclipse &"
6. Select the workspace: /home/vagrant/workspace
7. The HelloWorld project should be loaded. Build it by clicking the hammer toolbar icon.
8. The eclipse console tab shows HelloWorld was built using the aarch64 cross compiler.

To shutdown the VM, type "vagrant halt" in the PowerShell window.
