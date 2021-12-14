How To Clone A Private Github Repo To A cPanel Server
Git private repository requires SSH access.

So you must ensure that your hosting package has SSH enabled (customers on Web Hosting Magic need not worry as every hosting package comes with SSH access) and perform additional steps in order to successfully clone a privately-hosted remote repository to your cPanel server.

You can use cPanel's Terminal interface (cPanel >> Home >> Advanced >> Terminal) to access the command line from within the cPanel interface.

You can also use your local system's Terminal or any tool that allows you to access the cPanel server via SSH.

1. Generate An SSH Key

If you have not already configured one, run the following command to generate an SSH key:

ssh-keygen -t rsa -b 4096 -C "username@example"
In this example, "username" represents the cPanel account username and "example" represents the domain name.

After you run this command, the system will prompt you to enter a passphrase.

Do not enter a passphrase.

Press Enter to continue.

2. Verify That You Generated The Ssh Key Correctly

To confirm that the key exists and is in the correct location, run the following command:

cat ~/.ssh/id_rsa.pub
3. Register Your SSH Key With The Private Repository Host

For information about how to register your SSH key with another private repository host (Bitbucket, GitLab, etc), consult that host's website or documentation.

Some repository hosts, such as Bitbucket, do not allow you to configure write access for your access keys.

To register an SSH key with GitHub, perform the following steps:

Log in to your GitHub account.
Navigate to your private repository.
In the top right corner of the page, click Settings. A new page will appear.
In the left side menu, click Deploy keys. A new page will appear.
In the top right corner of the page, click Add deploy key. A new page will appear.
Enter your SSH key data:
In the Title text box, enter a display name for the key.
In the Key text box, paste the entire SSH key. If you want to push code from your cPanel account to your GitHub account, select the "Allow write access" checkbox. Do note that if you do not select this checkbox, you can only deploy changes from your GitHub repository to the cPanel-hosted repository.
Click Add key.
4. Test Out The SSH Key

To test your SSH key, run the following command.

ssh -T git@example.com
where example.com represents the private repository's host - e.g ssh -T git@github.com.

5. Clone The Private Repo

To clone the repository, run the following command on the cPanel account, where "git clone git@example.com:$name/private-repo.git" represents the private repository's clone URL:

git clone git@example.com:$name/private-repo.git
If you see Error: The WebSocket handshake failed at ... when you access cPanel's Terminal interface (cPanel >> Home >> Advanced >> Terminal), recheck your connect.

If you are using VPN, disconnect and use your normal internet connection.
