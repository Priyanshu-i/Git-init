```ssh
$ git config --global user.name "Priyanshu Singh"
$ git config --global user.email "priyanshu40507@gmail.com
$ git config --list
```
Great! Here are the detailed steps tailored for Windows 11 to generate an SSH key, add it to GitHub, and configure Git to use the SSH key:

### Step 1: Check for Existing SSH Keys
Open Git Bash and run the following command to see if any SSH keys already exist:

```bash
ls -al ~/.ssh
```

If you see files like `id_rsa` and `id_rsa.pub`, you already have an SSH key pair. If not, proceed to generate a new one.

### Step 2: Generate a New SSH Key
If you don't have an SSH key pair or want to create a new one, generate a new SSH key:

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

If you are using a legacy system that doesn't support the `ed25519` algorithm, use:

```bash
ssh-keygen -t rsa -b 4096 -C "your.email@example.com"
```

When prompted to "Enter a file in which to save the key," press Enter to accept the default file location (`/c/Users/your_user/.ssh/id_ed25519` or `/c/Users/your_user/.ssh/id_rsa`).

When prompted for a passphrase, type a secure passphrase or press Enter for no passphrase.

### Step 3: Add the SSH Key to the SSH Agent
Start the SSH agent in the background:

```bash
eval "$(ssh-agent -s)"
```

Add your SSH private key to the SSH agent:

```bash
ssh-add ~/.ssh/id_ed25519
```

If you used `rsa`, the command would be:

```bash
ssh-add ~/.ssh/id_rsa
```

### Step 4: Add the SSH Key to Your GitHub Account
1. **Copy the SSH key to your clipboard**:
   
   In Git Bash, use the following command to copy the SSH key to your clipboard:

   ```bash
   clip < ~/.ssh/id_ed25519.pub
   ```

   If you used `rsa`, the command would be:

   ```bash
   clip < ~/.ssh/id_rsa.pub
   ```

2. **Log in to GitHub**:
   Go to [GitHub](https://github.com/) and log in.

3. **Navigate to SSH and GPG keys settings**:
   - In the upper-right corner of any page, click your profile photo, then click **Settings**.
   - In the user settings sidebar, click **SSH and GPG keys**.

4. **Add a new SSH key**:
   - Click **New SSH key** or **Add SSH key**.
   - In the "Title" field, add a descriptive label for the new key (e.g., "My Windows 11 PC").
   - Paste your key into the "Key" field.
   - Click **Add SSH key**.
   - Confirm your GitHub password if prompted.

### Step 5: Test the Connection
To ensure everything is set up correctly, run:

```bash
ssh -T git@github.com
```

You might see a message like this:

```plaintext
The authenticity of host 'github.com (IP ADDRESS)' can't be established.
RSA key fingerprint is SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type `yes` and press Enter.

If you see:

```plaintext
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

You have successfully set up your SSH key.

### Step 6: Change Remote URL to Use SSH
If you initially set up your remote repository using HTTPS, you can change it to SSH.

1. **Check your current remote URL**:

   ```bash
   git remote -v
   ```

2. **Change the URL to SSH**:

   ```bash
   git remote set-url origin git@github.com:username/repo-name.git
   ```

Replace `username` with your GitHub username and `repo-name` with the name of your repository.

Now, you can use Git commands like `git push` and `git pull` without entering your username and password each time.
