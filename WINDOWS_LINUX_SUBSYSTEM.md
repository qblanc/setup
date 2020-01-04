_DISCLAIMER We heavily recommend a minimal hardware configuration to consider this Windows Linux Subsystem setup: A SSD drive and at least 8Go RAM are mandatory_


# Setup instructions

The following instructions will help you to get ready for [Le Wagon](http://www.lewagon.org) fullstack bootcamp:

- Grab a text editor, where you'll spend your day and nights
- Install a package manager
- Pimp your Terminal
- Setup git and GitHub
- Install Ruby


## Prerequisites

First you need to check your machine runs on Windows 10 build 1615 or later. Follow theses steps to [check your build](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#check-your-build-number). For earlier versions of Windows 10, follow [Le Wagon Windows setup](WINDOWS.md).

### Ubuntu on Windows

Press `Windows key`, then type `powershell`. Right click on `Windows PowerShell (x86)` then click on `Run as administrator`
A blue window will open, run the following command in it:
```bash
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
The terminal will offer you to restart your computer, type `y` and press `Enter`.

Download [Ubuntu on Windows](https://www.microsoft.com/fr-fr/store/p/ubuntu/9nblggh4msv6?rtc=1) from the Windows Store. Once download has completed, select _Launch_. This will open a console window. Wait for installation to complete then you will be prompted to create your LINUX user account. Create your LINUX username and password. This user account has no relationship to your Windows username and password and hence can be different.

You're now ready to use your Linux environment 👏.

To open a terminal, press `Windows key`, then type `Ubuntu` (it might show up earlier, though), then `Enter`

You will have to copy-paste a lot of commands in this guide. While copying to the clipboard works as everywhere else by selecting the text, and pressing `Ctrl` + `C`, pasting into the terminal is done by right-clicking anywhere within the terminal window.

Start with this command that installs a few useful utilities that will be needed later:
```bash
sudo apt update
sudo apt install -y apt-transport-https unzip gnome-terminal
```

:point_up: This command will ask for your password with: `[sudo] password for <username>:`. The Linux terminal won't give you any feedback, like `\*`, as you might be used to. You just have to type it correctly, and then press `Enter`. If you type it wrong, you will be asked again otherwise the terminal will remember it until it is closed.

### Menlo for Powerline font

Menlo for Powerline is a fancy font for your terminal. Download it from [abertsch/Menlo-for-Powerline repository](https://github.com/abertsch/Menlo-for-Powerline/raw/master/Menlo%20for%20Powerline.ttf) on GitHub. Once download has completed, double-click on the `Menlo for Powerline.ttf` file and install it on windows.

Then open a terminal and right-click on the Ubuntu logo then choose `>Settings>Fonts>Menlo for Powerline` and save.

## GitHub account

Have you signed up to GitHub? If not, [do it right away](https://github.com/join).

:point_right: **[Upload a picture](https://github.com/settings/profile)** and put your name correctly on your GitHub account. This is important as we'll use an internal dashboard with your avatars. Please do it **now**.


## Git

To install `git`, first open a terminal. To open a terminal, you can click on the Ubuntu Start button in the sidebar and type `Terminal`. Then click on the terminal icon.

Then copy this line with `Ctrl` + `C`:

```bash
sudo apt install -y git
```

## Oh-my-zsh - Fancy your Terminal

We will use the shell named `zsh` instead of `bash`, the default one.

```bash
sudo apt install -y zsh curl vim imagemagick jq
```

We need to install the latest version of nodejs:
```bash
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt install -y nodejs
```

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
# it will ask for your session password
```

Be careful, those commands will ask you to type your password twice. At the end
your prompt should look like this:

![](images/ubuntu_oh_my_zsh.png)

If it doesn't, **ask a teacher**.

To make this change stick, close your terminal and open it again.

## GitHub

We need to generate SSH keys which are going to be used by GitHub and Heroku
to authenticate you. Think of it as a way to log in, but different from the
well known username/password couple. If you already generated keys
that you already use with other services, you can skip this step.

Open a terminal and type this, replacing the email with **yours** (the
same one you used to create your GitHub account). It will prompt
for information. Just press enter until it asks for a **passphrase**.

```bash
mkdir -p ~/.ssh && ssh-keygen -t ed25519 -o -a 100 -f ~/.ssh/id_ed25519 -C "TYPE_YOUR_EMAIL@HERE.com"
```

**NB:** when asked for a passphrase, put something you want (and that you'll remember),
it's a password to protect your private key stored on your hard drive. You'll type,
nothing will show up on the screen, **that's normal**. Just type the passphrase,
and when you're done, press `Enter`.

Then you need to give your **public** key to GitHub. Run:

```bash
cat ~/.ssh/id_ed25519.pub
```

It will prompt on the screen the content of the `id_ed25519.pub` file. Copy that text,
then go to [github.com/settings/ssh](https://github.com/settings/ssh). Click on
**Add SSH key**, fill in the Title with your computer name, and paste the **Key**.
Finish by clicking on the **Add key** green button.

To check that this step is completed, in the terminal run this. You will be
prompted a warning, type `yes` then `Enter`.

```bash
ssh -T git@github.com
```

If you see something like this, you're done!

```bash
# Hi --------! You've successfully authenticated, but GitHub does not provide shell access
```

If it does not work, try running this before trying again the `ssh -T` command:

```bash
ssh-add ~/.ssh/id_ed25519
```

Don't be in a rush, take time to [read this article](http://sebastien.saunier.me/blog/2015/05/10/github-public-key-authentication.html) to get a better
understanding of what those keys are used for.


## Dotfiles (Standard configuration)

Hackers love to refine and polish their shell and tools. We'll start with a great default configuration provided by [Le Wagon](http://github.com/lewagon/dotfiles), stored on GitHub. As your configuration is personal, you need your own repository storing it, so you first need to fork it to your GitHub account.

:arrow_right: [Click here to **fork**](https://github.com/lewagon/dotfiles/fork) the `lewagon/dotfiles` repository to your account.

You should arrive on a page that looks like this. Make sure to **select your GitHub account**.

![](images/fork.png)

Forking means that it will create a new repo in your GitHub account, identical to the original one. You'll have a new repository on your GitHub account, `your_github_username/dotfiles`. We need to fork because each of you will need to put specific information (e.g. your name) in those files.

Open your terminal. **Don't blindly copy paste this line**, replace `replace_this_with_your_github_username` with *your*
own github usernickname.

```bash
export GITHUB_USERNAME=replace_this_with_your_github_username

# Example:
#   export GITHUB_USERNAME=ssaunier
```

Now copy/paste this very long line in your terminal. Do **not** change this one.

```bash
mkdir -p ~/code/$GITHUB_USERNAME && cd $_ && git clone git@github.com:$GITHUB_USERNAME/dotfiles.git
```

Run the `dotfiles` installer.

```bash
cd ~/code/$GITHUB_USERNAME/dotfiles
zsh install.sh
```

Then run the git installer:

```bash
cd ~/code/$GITHUB_USERNAME/dotfiles
zsh git_setup.sh
```

:point_up: This will **prompt** you for your name (`Firstname Lastname`) and your email.

Be careful, you **need** to put the **same** email as the one you sign up with on GitHub.

You need to prepend commands that start applications in a graphical interface outside the command line with `DISPLAY=:0 `, e.g. `DISPLAY=:0 subl`, or set this variable by adding it to `~/.bashrc`, i.e.
```bash
echo "export DISPLAY=:0" >> ~/.bashrc
echo "export DISPLAY=:0" >> ~/.zshrc
```

We also need to install a graphical library:
```bash
sudo apt install libgtk2.0-0
```
Restart your terminal.

### Auto-start `ssh-agent`

You don't want to be asked for your passphrase every time you communicate with a distant repository. So you need to add the plugin `ssh-agent` to `oh my zsh`.
First open `.zshrc` file:

```bash
stt ~/.zshrc
```

Spot the line starting with `plugins=` Then add `ssh-agent` to the plugins list. The list should look like:

```
plugins=(gitfast last-working-dir common-aliases sublime zsh-syntax-highlighting history-substring-search ssh-agent)
```

Save the `.zshrc` file with `Ctrl` + `S` and you can close Sublime Text.



