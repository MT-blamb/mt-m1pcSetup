# Moneytree Mac with M1 chip setup guide
A comprehensive guide for setting up an M1 chipped machine for work at Moneytree
   
# Setup instructions

You will find below the instructions to set up you computer for [Moneytree's Link Data team](https://moneytree-app.atlassian.net/wiki/spaces/LD/pages/1430847489/Introduction+to+LINK+Data).

Please **read them carefully and execute all commands in the following order**.

If you get stuck, don't hesitate to ask a teammate for help :raising_hand:

You can also have a look at [some cheatsheets](https://github.com/lewagon/setup/tree/master/docs) for common issue fixes and tips :heavy_check_mark:

Let's start :rocket:


## M1 silicon chips

If you have a Mac with Apple silicon, [you are asked to install Rosetta](https://support.apple.com/en-us/HT211861). Click Install, then enter your user name and password to allow installation to proceed.

![Install Rosetta](https://support.apple.com/library/content/dam/edam/applecare/images/en_US/macos/Big-Sur/macos-big-sur-software-update-rosetta-alert.jpg)

Please also make sure you setup what we will call a Rosetta-terminal.
Go to Finder > Applications > Utilities 
![image](https://user-images.githubusercontent.com/102956235/163519416-57d4ce63-235a-4d29-9e64-0a8380b26635.png)

Right click on Terminal and open options:

![image](https://user-images.githubusercontent.com/102956235/163519500-e7d5878f-5306-4850-8714-ee3276598608.png)

![image](https://user-images.githubusercontent.com/102956235/163519568-add253c7-792a-453b-bcf7-d99186339e3e.png)

Select Duplicate and rename the new terminal to Rosetta-terminal, click Get Info and check 'Open Using Rosetta' ✔.

Congratulations, you now have a Rosetta-terminal that will allow you to install/run things from the old Intel x86_64 architecture.

From now on please install and run things using your Rosetta-terminal. The reason for this is that certain projects use older architecture implementations that are not able to run properly on the new M1 `arm64` architecture. In your Rosetta-terminal when you type `arch` and press `enter` it should output `i386`. If it outputs `arm64` you are in the wrong terminal and things will not install correctly down the line. Please contact a team member if you are having trouble setting up a Rosetta-terminal.

## GitHub account

Have you signed up to GitHub with your Moneytree email? If not, [do it right away](https://github.com/join).

:point_right: **[Upload a picture](https://github.com/settings/profile)** and put your name correctly using this format: **mt-[your moneytree email]** on your GitHub account. This is important as we'll use an internal dashboard with your avatar. Please do this **now**, before you continue with this guide.

You may also want to use the Yubikey as a security key for 2FA
Send account to Sergio for GitHub moneytree-organisation invitation


## SSH Key For GitHub
1. Open up a Rosetta-Terminal window and run:

```bash
ssh-keygen
```

2. Press enter after the first prompt to accept the default file to save the key (/Users/[you]/.ssh/id_rsa). Then enter a suitable passphrase. After this command finishes, run:

```bash
cat ~/.ssh/id_rsa.pub
```

and copy the output to the clipboard.

3. Go back to Github.com account settings.  Click “SSH Keys”.  Add a new key with the value on your clipboard from step (1).


## A note about quitting apps on a Mac

Clicking the little red cross in the top left corner of the application window on a Mac **does not really quit it**, it just closes an active window. To quit the application _for real_ either press `Cmd + Q` when the application is active, or navigate to `APP_NAME` -> `Quit` in the menu bar.

![image](https://user-images.githubusercontent.com/102956235/163535412-12893599-08cd-452b-878b-c2eb01106144.png)

During this setup you will be asked to **quit and re-open** applications multiple times, please make sure you do it properly :pray:

## Command Line Tools

Open a new Rosetta-terminal, copy-paste the following command and hit `Enter`:

```bash
xcode-select --install
```

If you receive the following message, you can just skip this step and go to next step.

```bash
# command line tools are already installed, use "Software Update" to install updates
```

Otherwise, it will open a window asking you if you want to install some software: click on "Install" and wait.


![image](https://user-images.githubusercontent.com/102956235/163535881-e7595367-bf7b-48f1-aa11-e1829d6e5454.png)

:heavy_check_mark: If you see the message "The software was installed" then all good :+1:

:x: If the command `xcode-select --install` fails try again: sometimes the Apple servers are overloaded.

:x: If you see the message "Xcode is not currently available from the Software Update server", you need to update the software update catalog:

```bash
sudo softwareupdate --clear-catalog
```

Once this is done, you can try to install again.


## Homebrew

[Homebrew](http://brew.sh/) is a package manager: it's a software used to install other software from the command line. Let's install it!

Open a Rosetta-terminal and run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

This will ask for your confirmation (hit `Enter`) and your **macOS user account password** (the one you use to [log in](https://support.apple.com/en-gb/HT202860) when you reboot your Macbook).

:warning: When you type your password, nothing will show up on the screen, **that's normal**. This is a security feature to mask not only your password as a whole but also its length. Just type your password and when you're done, press `Enter`.

:warning: If you already have Homebrew, it will tell you so, please make sure it is the Intel architecture version. The intel version will have created folders like `/user/local` whereas the Arm architecture will create files like `/opt/usr/local`. If you are unsure if you have the right version of Homebrew installed please run this command to uninstall it:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall.sh)"
```

Then install some useful software:

```bash
brew update
```

If you get a `/usr/local must be writable` error, just run this:

```bash
sudo chown -R $USER:admin /usr/local
brew update
```


## Visual Studio Code

### Installation

Let's install [Visual Studio Code](https://code.visualstudio.com) text editor.

Copy (`Cmd` + `C`) the command below then paste it in your Rosetta-terminal (`Cmd` + `V`):

```bash
brew install --cask visual-studio-code
```

Then launch VS Code by running the following command in your Rosetta-terminal:

```bash
code
```

:heavy_check_mark: If a VS Code window has just opened, you're good to go :+1:

:x: Otherwise, please **contact a team member**


## VS Code Extensions

### Installation

Let's install some useful extensions to VS Code.

Copy-paste the following commands in your Rosetta-terminal:

```bash
code --install-extension ms-vscode.sublime-keybindings
code --install-extension emmanuelbeziat.vscode-great-icons
code --install-extension MS-vsliveshare.vsliveshare
code --install-extension rebornix.ruby
code --install-extension dbaeumer.vscode-eslint
code --install-extension Rubymaniac.vscode-paste-and-indent
code --install-extension alexcvzz.vscode-sqlite
```

:warning: If you recieve a `zsh` error message telling you `code` doesn't work as a command please open VScode and press **`⌘`+`↑`+`P`** and refer to this picture:

![image](https://user-images.githubusercontent.com/102956235/163538711-36b3314b-e10a-4cd7-a8eb-9a37514daa11.png)

Just begin to type in `User shell command` and then click the shell command to uninstall and then reinstall the shell command for `code`.

Here is a list of the extensions you are installing:
- [Sublime Text Keymap and Settings Importer](https://marketplace.visualstudio.com/items?itemName=ms-vscode.sublime-keybindings)
- [VSCode Great Icons](https://marketplace.visualstudio.com/items?itemName=emmanuelbeziat.vscode-great-icons)
- [Live Share](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare)
- [Ruby](https://marketplace.visualstudio.com/items?itemName=rebornix.Ruby)
- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [Paste and Indent](https://marketplace.visualstudio.com/items?itemName=Rubymaniac.vscode-paste-and-indent)
- [SQLite](https://marketplace.visualstudio.com/items?itemName=alexcvzz.vscode-sqlite)

That's it, you're good to go!

Error message or not, proceed running the following in the Rosetta-terminal (you can copy / paste all the lines at once).

```bash
brew upgrade git || brew install git
brew upgrade gh || brew install gh
brew upgrade wget || brew install wget
brew upgrade imagemagick || brew install imagemagick
brew upgrade jq || brew install jq
```

## A note about openssl

:warning: The reason we did not include a `brew install openssl` command above is due to the fact that some of the versions of tools we use (ie `Ruby 2.3.3`) in some of our projects (SSU) relies on an older version of `openssl` (`openssl@1.0.2u`) that is no longer directly available via `Brew`.

To install this older version of `openssl` we need to do a few things. 

1. We need to make a file that we will call `openssl@1.0.rb` on our Desktop. You can do this through VSCode.
2. We need to add this to the contents of that file:
 ```bash
 # Extraced from pre- https://github.com/Homebrew/homebrew-core/pull/46876
class OpensslAT10 < Formula
    desc "SSL/TLS cryptography library"
    homepage "https://openssl.org/"
    url "https://www.openssl.org/source/openssl-1.0.2u.tar.gz"
    mirror "https://www.mirrorservice.org/sites/ftp.openssl.org/source/openssl-1.0.2u.tar.gz"
    sha256 "ecd0c6ffb493dd06707d38b14bb4d8c2288bb7033735606569d8f90f89669d16"
  
    keg_only :provided_by_macos,
      "Apple has deprecated use of OpenSSL in favor of its own TLS and crypto libraries"
  
    # Add darwin64-arm64-cc & debug-darwin64-arm64-cc build targets.
    patch :DATA
  
    def install
      # OpenSSL will prefer the PERL environment variable if set over $PATH
      # which can cause some odd edge cases & isn't intended. Unset for safety,
      # along with perl modules in PERL5LIB.
      ENV.delete("PERL")
      ENV.delete("PERL5LIB")
  
      ENV.deparallelize
      args = %W[
        --prefix=#{prefix}
        --openssldir=#{openssldir}
        no-ssl2
        no-ssl3
        no-zlib
        shared
        enable-cms
        darwin64-#{Hardware::CPU.arch}-cc
        enable-ec_nistp_64_gcc_128
      ]
      system "perl", "./Configure", *args
      system "make", "depend"
      system "make"
      system "make", "test"
      system "make", "install", "MANDIR=#{man}", "MANSUFFIX=ssl"
    end
  
    def openssldir
      etc/"openssl"
    end
  
    def post_install
      keychains = %w[
        /System/Library/Keychains/SystemRootCertificates.keychain
      ]
  
      certs_list = `security find-certificate -a -p #{keychains.join(" ")}`
      certs = certs_list.scan(
        /-----BEGIN CERTIFICATE-----.*?-----END CERTIFICATE-----/m,
      )
  
      valid_certs = certs.select do |cert|
        IO.popen("#{bin}/openssl x509 -inform pem -checkend 0 -noout", "w") do |openssl_io|
          openssl_io.write(cert)
          openssl_io.close_write
        end
  
        $CHILD_STATUS.success?
      end
  
      openssldir.mkpath
      (openssldir/"cert.pem").atomic_write(valid_certs.join("\n") << "\n")
    end
  
    def caveats; <<~EOS
      A CA file has been bootstrapped using certificates from the SystemRoots
      keychain. To add additional certificates (e.g. the certificates added in
      the System keychain), place .pem files in
        #{openssldir}/certs
  
      and run
        #{opt_bin}/c_rehash
    EOS
    end
  
    test do
      # Make sure the necessary .cnf file exists, otherwise OpenSSL gets moody.
      assert_predicate HOMEBREW_PREFIX/"etc/openssl/openssl.cnf", :exist?,
              "OpenSSL requires the .cnf file for some functionality"
  
      # Check OpenSSL itself functions as expected.
      (testpath/"testfile.txt").write("This is a test file")
      expected_checksum = "e2d0fe1585a63ec6009c8016ff8dda8b17719a637405a4e23c0ff81339148249"
      system "#{bin}/openssl", "dgst", "-sha256", "-out", "checksum.txt", "testfile.txt"
      open("checksum.txt") do |f|
        checksum = f.read(100).split("=").last.strip
        assert_equal checksum, expected_checksum
      end
    end
  end
  
```
3. Now we need to run this command in the Rosetta-terminal: 

```bash
brew install ~/Desktop/openssl@1.0.rb
```

Congratulations you just installed an ancient, but as of the time of writing, necessary version of `openssl` :rocket:

## macOS Rosetta-Terminal Theme

Launch a Rosetta-terminal, click on `Terminal > Preferences` and set the "Pro" theme as default profile.

<img width="389" alt="image" src="https://user-images.githubusercontent.com/102956235/163548704-d888f751-47f2-4305-9bf7-ff5e463d46b3.png">
<img width="685" alt="image" src="https://user-images.githubusercontent.com/102956235/163548749-a8f8cac0-9b3b-4586-8d22-1d8db1df9fad.png">

**Quit and restart** your Rosetta-terminal: it should now have a nice black background, easier on the eyes.


## Oh-my-zsh

Let's install the `zsh` plugin [Oh My Zsh](https://ohmyz.sh/).

In a Rosetta-terminal execute the following command:

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

If asked "Do you want to change your default shell to zsh?", press `Y`

At the end your Rosetta-terminal should look like this:

<img width="576" alt="image" src="https://user-images.githubusercontent.com/102956235/163552559-26536dc8-75d6-4e10-9ec1-c44826dca090.png">

:heavy_check_mark: If it does, you can continue :+1:

:x: Otherwise, please **ask for a team member** You can also try:

```bash
omz update
```

This will either update or fail. If it fails please try installing again or contact a team member for help 🧑‍🚀

## GitHub CLI

CLI is the acronym of [Command-line Interface](https://en.wikipedia.org/wiki/Command-line_interface).

In this section, we will use [GitHub CLI](https://cli.github.com/) to interact with GitHub directly from the Rosetta-terminal.

It should already be installed on your computer from the previous commands. Let's check that really quick :rabbit:

To check that you are properly connected, type:

```bash
gh auth status
```

:heavy_check_mark: If you get `Logged in to github.com as <YOUR USERNAME> `, then all good :+1:

:x: If not, **contact a team member**.

Open your Rosetta-terminal and run the following commands:

```bash
export GITHUB_USERNAME=`gh api user | jq -r '.login'`
echo $GITHUB_USERNAME
```

:heavy_check_mark: You should see your GitHub username printed.

:x: If not, **stop here** and ask for help. There may be a problem with the previous step (`gh auth`).

You may need to **login**, copy-paste the following command in your Rosetta-terminal:

:warning: **DO NOT edit the `email`**

```bash
gh auth login -s 'user:email' -w
```

gh will ask you few questions:

`What is your preferred protocol for Git operations?` With the arrows, choose `SSH` and press `Enter`. SSH is a protocol to log in using SSH keys instead of the well known username/password pair.

`Generate a new SSH key to add to your GitHub account?` Press `Enter` to ask gh to generate the SSH keys for you.

If you already have SSH keys, you will see instead `Upload your SSH public key to your GitHub account?` With the arrows, select your public key file path and press `Enter`.

`Enter a passphrase for your new SSH key (Optional)`. Type something you want and that you'll remember. It's a password to protect your private key stored on your hard drive. Then press `Enter`.

:warning: When you type your passphrase, nothing will show up on the screen, **that's normal**. This is a security feature to mask not only your passphrase as a whole but also its length. Just type your passphrase and when you're done, press `Enter`.

You will then get the following output:

```bash
! First copy your one-time code: 0EF9-D015
- Press Enter to open github.com in your browser...
```

Select and copy the code (`0EF9-D015` in the example), then press `Enter`.

Your browser will open and ask you to authorize GitHub CLI to use your GitHub account. Accept and wait a bit.

Come back to the Rosetta-terminal, press `Enter` again, and that's it.

Please now **reset** your Rosetta-terminal by running:

```bash
exec zsh
```
OR

```bash
source ~/.zhrc
```

## rbenv

Let's install [`rbenv`](https://github.com/sstephenson/rbenv), a software to install and manage `ruby` environments.

First, we need to clean up any previous Ruby installation you might have:

```bash
rvm implode && sudo rm -rf ~/.rvm
# If you got "zsh: command not found: rvm", carry on. It means `rvm` is not
# on your computer, that's what we want!
sudo rm -rf $HOME/.rbenv /usr/local/rbenv /opt/rbenv /usr/local/opt/rbenv
```

:warning: This command may prompt for your password.

:warning: When you type your password, nothing will show up on the screen, **that's normal**. This is a security feature to mask not only your password as a whole but also its length. Just type your password and when you're done, press `Enter`.

In the Rosetta-terminal, run:

```bash
brew uninstall --force rbenv ruby-build
exec zsh
```

Then run:

```bash
brew install rbenv
```

Now please open your zsh file.
To your zsh file. To open your zsh file enter this in your Rosetta-terminal:

```bash
code ~/.zshrc
```
Add this line to the bottom of your `zsh` file:

```bash
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
```

## Ruby

### Installation

Now, you are ready to install the latest [ruby](https://www.ruby-lang.org/en/) version and set it as the default version.

Run this command, it will **take a while (5-10 minutes)**

```bash
rbenv install 3.0.3
```

Once the ruby installation is done, run this command to install an older version of Ruby necessary for SSU development at the time of writing:

```bash
rbenv install 2.3.3
```

**Reset** your Rosetta-terminal and check your Ruby version:

```bash
exec zsh
```

Then run:

```bash
ruby -v
```

:heavy_check_mark: If you see something starting with `ruby 3.0.3p` or `ruby 2.3.3` then you can proceed +1:

:x: If not, **ask a team member**

### Installing some gems

<details>
  <summary>If you are in <bold>China</bold> 🇨🇳 click here</summary>

  :warning: If you are in China, you should update the way we'll install gem with the following commands.

```bash
# China only!
gem sources --remove https://rubygems.org/
gem sources -a https://gems.ruby-china.com/
gem sources -l
# *** CURRENT SOURCES ***
# https://gems.ruby-china.com/
# Ruby-china.com must be in the list now
```
</details>

**Everyone, in China or not**, continue here to install gems.

In the ruby world, we call external libraries `gems`: they are pieces of ruby code that you can download and execute on your computer. Let's install some!

In your Rosetta-terminal, copy-paste the following command:

```bash
gem install rake rspec rubocop-performance pry-byebug colored http 'rails:~>6.1'
```

:heavy_check_mark: If you get `xx gems installed`, then all good :+1:

:x: If you encounter the following error:

```bash
ERROR: While executing gem ... (TypeError)
incompatible marshal file format (can't be read)
format version 4.8 required; 60.33 given
```
Run the following command:
```bash
rm -rf ~/.gemrc
```
Rerun the command to install the gems.
:warning: **NEVER** install a gem with `sudo gem install`! Even if you stumble upon a Stackoverflow answer (or the Rosetta-terminal) telling you to do so.

## Special note about Bundler and SSU
SSU development will need you to install a special version of bundler:
```bash
gem install bundler 1.17.3
```

## Node.js
[Node.js](https://nodejs.org/en/) is a JavaScript runtime to execute JavaScript code in the Rosetta-terminal. Let's install it with [nvm](https://github.com/nvm-sh/nvm), a version manager for Node.js.
In a Rosetta-terminal, execute the following commands:
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | zsh
exec zsh
```

OR simply

```bash
brew install nvm
```
Then run the following command:
```bash
nvm -v
```
You should see a version. If not, ask a team member.
Now let's install node:
```bash
nvm install 17.8.0
```
When the installation is finished, run:
```bash
node -v
```
If you see `v17.8.0`, the installation succeeded :heavy_check_mark: You can then run:
```bash
nvm cache clear
```
:x: If not, **contact a team member**

## Python
	Let's install and control our python version with pyenv
  First let's enter this into our Rosetta-terminal:

```bash
brew install pyenv
```

Now please open your zsh file.
To your zsh file. To open your zsh file enter this in your Rosetta-terminal:

```bash
code ~/.zshrc
```
Add this line to the bottom of your `zsh` file:

```bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
```
When you are in a work project's repository, use the `pyenv install`, by default it will use `.python-version` in the project's directory.

Congratulations you just installed `pyenv` and are totally ready to install python versions when you get into a project! :rocket:

## yarn
[`yarn`](https://yarnpkg.com/) is a package manager to install JavaScript libraries. Let's install it:
In a Rosetta-terminal, run the following commands:

```bash
brew install yarn
```

Then run the following command:
```bash
yarn -v
```
:heavy_check_mark: If you see a version, you're good :+1:
:x: If not, **ask for a team member**

## PostgreSQL
Sometimes, SQLite is not enough and we will need a more advanced tool called [PostgreSQL](https://www.postgresql.org/), an open-source robust and production-ready database system. 

We use an older version of Postgres for work, though. We need version 9.6. So the installation might seem a bit unrefined:

A. Install 9.6 from http://postgresapp.com/documentation/all-versions.html
Do not use the latest (to be compatible with the production DB)

Make sure postgres version you installed (9.6)

B. Install 9.6 via Homebrew (recommended if available)

```bash
brew install  postgresql@9.6
```
Now please open your zsh file.
To your zsh file. To open your zsh file enter this in your Rosetta-terminal:

```bash
code ~/.zshrc
```

Now copy and paste this to the very bottom of your zsh file: 

```bash
PATH=$PATH:/Applications/Postgres.app/Contents/Versions/9.6/bin to 
```

Reset your terminal and try this:

```bash
postgres --version
```

If you get a message like this you're good to go :+1:

<img width="184" alt="image" src="https://user-images.githubusercontent.com/102956235/163555663-2a74c750-80d4-4824-ab81-ed3043b50f0b.png">


Otherwise please contact a team member.

## AWS Vault & MFA
Please open up your Rosetta-terminal and run:
```bash
brew install --cask install aws-vault
```
1. On the AWS Management Console, go to My Security Credentials, set up MFA and create access key.
MFA - Make sure under “Multi-factor authentication (MFA)” you have a (Virtual) MFA device set up. Do not use your Yubikey for this. We recommend using the mobile app Authy to keep track of your tokens. 

2. MFA - Make sure under “Multi-factor authentication (MFA)” you have a (Virtual) MFA device set up. Do not use your Yubikey for this. We recommend using the mobile app Authy to keep track of your tokens. After you have MFA setup you should see something similar to this on the Security Credentials page:

![image](https://user-images.githubusercontent.com/102956235/163558457-e97e656b-ce30-4c9c-a474-c8d3435b481e.png)

3. Access Key - Create one and keep the key and the secret somewhere safe. I recommend LastPass.

Then run 
```bash
aws-vault add default YOUR_ACCESS_KEY
```
Lastly it will prompt you for secret key (when you created access key it will show you a place to click for secret key)

## AWS Command Line Tools
In your Rosetta-terminal please run:
```bash
brew install awscli
```

Now please open your zsh file.
To your zsh file. To open your zsh file enter this in your Rosetta-terminal:

```bash
code ~/.zshrc
```

Now copy and paste this to the very bottom of your zsh file: 

```bash
complete -C aws_completer aws
```
## AWS configure
Follow [step 3](https://github.com/moneytree/mt-infra-iam) to add **development, staging and production** as needed.

* A note about AWS: You will need to log out and log back in after enabling MFA to be able to switch/add IAM roles to your profile.

## Check-up
When you run:
```bash
aws configure list
```
You should hopefully be seeing something like this:

<img width="549" alt="image" src="https://user-images.githubusercontent.com/102956235/163559507-5f5b0462-ef5e-4b45-9e49-60a02bbe581e.png">

And when you run:
```bash
aws-vault list
```
You should be seeing something like this:

<img width="549" alt="image" src="https://user-images.githubusercontent.com/102956235/163559582-1a5fa390-e7e4-4475-a248-21af4e002655.png">

And when you run:
```bash
cat ~/.aws/credentials
```
You should be seeing your `aws_access_key_id` and your `aws_secret_access_key` under `[default]`.

### Keyboard
As you become a programmer, you'll understand that leaving the keyboard takes a lot of time, so you'll want to minimize using the trackpad or the mouse. Here are a few tricks on macOS to help you do that.
#### Keyboard speed
Go to ` > System Preferences > Keyboard`. Set `Key Repeat` to the fastest position (to the right) and `Delay Until Repeat` to the shortest position (to the right).
#### Full Keyboard Access
Go to ` > System Preferences > Keyboard`. Click on the third tab `Shortcuts`. At the bottom of the pane, click the radio button `All controls`. This way when you get a dialog with several options, you'll be able to type `Enter` to confirm, or `SPACE` to choose the cancel option. If you have more than two options, you can use tab to circle between them.
#### macOS For hackers
[Read this script](https://github.com/mathiasbynens/dotfiles/blob/master/.macos) and cherry-pick some stuff you think will suit you. For instance, you can type in the Rosetta-terminal this one:
```bash
# Expanding the save panel by default
defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode -bool true
defaults write NSGlobalDomain PMPrintingExpandedStateForPrint -bool true
defaults write NSGlobalDomain PMPrintingExpandedStateForPrint2 -bool true
# Save screenshots to the Desktop (or elsewhere)
defaults write com.apple.screencapture location "${HOME}/Desktop"
# etc..
```
### Pin apps to your dock
You are going to use most of the apps you've installed today really often. Let's pin them to your dock so that they are just one click away!
To pin an app to your dock, launch the app, right-click on the icon in the taskbar to bring up the context menu and choose "Options" then "Keep in Dock".
![How to pin an app to the taskbar in macOS](images/macos_dock.png)
You must pin:
- Your Rosetta-terminal
- Your file explorer
- VS Code
- Your Internet browser
- Slack
- Zoom
## Setup completed!
Your computer is now all set for development with Moneytree :muscle: :clap:
Enjoy working with your team, you will nail it :rocket:
© 2022 GitHub, Inc.
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
