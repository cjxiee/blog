### Fix the error of removed support for password authentication of git remote

Generate a token for repo.

Once you have a token, you can enter it instead of your password when performing Git operations over HTTPS.

For example, on the command line you would enter the following:

    $ git clone https://github.com/username/repo.git
Username: your_username

Password: **your_token**

    #### try GitCredential Manager
<img width="881" alt="image" src="https://user-images.githubusercontent.com/89954165/198305903-8866c66c-34fa-465d-8b47-b070c2896889.png">


### To fix issues of entering username and password everytime git push

    $ set the remote origin as ssh
    $ git remote set-url origin "ssh link" 
    $ git push -u origin main

### Clone a repo with linked repo

    git clone --recursive ...
    
   
### Note: make install
    
    sudo make install       # install the lib to the default system path
    sudo make uninstall     # remove the installed lib
