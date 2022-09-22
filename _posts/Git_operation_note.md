# Fix the error of removed support for password authentication of git remote

Generate a token for repo.

Once you have a token, you can enter it instead of your password when performing Git operations over HTTPS.

For example, on the command line you would enter the following:

    $ git clone https://github.com/username/repo.git
Username: your_username

Password: **your_token**
