# GET STARTED PUNKPROTO

### Configure Github SendEmail

```
git config --global sendemail.smtpencryption tls
git config --global sendemail.smtpserver mail.messagingengine.com
git config --global sendemail.smtpuser punkproto@fastmail.com
git config --global sendemail.smtpserverport 587
git config --global sendemail.smtppass hackme
```

## Configuring the Default Destination Address

For PulseAudio, the patches should be sent to our mailing list. In order to avoid having to remember it and retyping it all the time, you can configure the address to be used by default by git send-email. As you may contribute to many projects using git, it does not make sense to set this option globally so instead we'll only set it in our clone of the PulseAudio code.

```
git config sendemail.to protopunk@einpunk.finance
```

## Avoiding sending mail to yourself

By default, git send-email will add the author of the patch to the Cc: field. When you send patches that you have written yourself, this means that a copy of each patch will be sent to your email address. If you don't like this, you can avoid this by setting this configuration option (see "git send-email --help" for the full list of possible values):

```
git config --global sendemail.suppresscc self
```

## Using the send-email Command

See "git send-email --help" for the full reference. I'll go through only the basic usage here.

git send-email will ask a few questions before the patches are sent (update: newer git versions ask fewer questions, sometimes no questions at all). Most of the questions have a sensible default value shown in square brackets. Just press enter to use the default value. Type the answer to the question if you don't want to use the default answer. The questions are:

Who should the emails appear to be from?
This will be used as the "From" header. You should have configured your name and email address earlier, so the default is usually correct.
Who should the emails be sent to?
As noted above, patches should be sent to our mailing list: pulseaudio-discuss@lists.freedesktop.org
Message-ID to be used as In-Reply-To for the first email?
This should usually be left empty. Don't send patches as replies to regular discussion, that makes it harder to keep track of the patches.
Send this email?
The mail headers are visible above the question, so that you can check that everything looks OK.

## Sending a Single Patch
Sending the last commit in the current branch:

```
git send-email -1
```
Sending some other commit:

git send-email -1 <commit reference>
Sending Multiple Patches
Sending the last 10 commits in the current branch:

git send-email -10 --cover-letter --annotate
The --cover-letter option creates an extra mail that will be sent before the actual patch mails. You can add write some introduction to the patch set in the cover letter. If you need to explain the patches, be sure to include the explanations also in the commit messages, because the cover letter text won't be recorded in the git history. If you don't think any introduction or explanation is necessary, it's fine to only have the shortlog that is included in the cover letter by default, and only set the "Subject" header to something sensible.

The --annotate option causes an editor to be started for each of the mails, allowing you to edit the mails. The option is always necessary, so that you can edit the cover letter's "Subject" header.

## Adding Patch Version Information

By default the patch mails will have "[PATCH]" in the subject (or "[PATCH n/m]", where n is the sequence number of the patch and m is the total number of patches in the patch set). When sending updated versions of patches, the version should be indicated: "[PATCH v2]" or "[PATCH v2 n/m]". To do this, use the -v option. Here's an example (you may want to add --annotate to add notes to the patch about what changed in the new version):

git send-email -v2 -1

## Changing or amending the [PATCH] tag in the subject

The default "[PATCH]" tag can be changed with --subject-prefix. This is useful especially when sending pavucontrol or paprefs patches, because the subject should note when the patch is meant for some other git repository than the main pulseaudio repository. For example:

```
# Using "[PATCH pavucontrol]" as the tag is a good way to indicate
# that the patch is meant for pavucontrol.
git send-email -1 --subject-prefix="PATCH pavucontrol"
Adding Extra Notes to Patch Mails
Sometimes it's convenient to annotate patches with some notes that are not meant to be included in the commit message. For example, one might want to write "I'm not sure if this should be committed yet, because..." in a patch, but the text doesn't make sense in the commit message. Such messages can be written below the three dashes "---" that are in every patch after the commit message. Use the --annotate option with git send-email to be able to edit the mails before they are sent.
```

## Formatting and sending in two steps

Instead of using the --annotate option, one can first run "git format-patch" to create text file(s) (with the -o option to select a directory where the text files are stored). These files can be inspected and edited, and when that is done, one can then use "git send-email" (without the -1 option) to send them.



## Setting up your development environment for macOS

This section provides a step-by-step guide for setting up your development environment on macOS.

MonoGame can work with most .NET compatible tools, but we recommend Visual Studio 2022 for Mac (prior versions are not supported).

Alternatively, you can use JetBrains Rider or Visual Studio Code.

## Install Visual Studio for Mac

Go to the following URL to download and install Visual Studio 2022 for Mac: https://visualstudio.microsoft.com/vs/mac/

## Install MonoGame extension for Visual Studio for Mac

Download the MonoGame extension for Visual Studio 2022 for Mac from the following link: https://github.com/MonoGame/MonoGame/releases/tag/v3.8.1

Open up Visual Studio 2022 for Mac and you should be able to see a window as shown below:

VS for Mac installer

In the menu bar, click on Visual Studio, and then click on the Extensions... menu item.

## Launch Extensions manager

Next, click on the Install from file... button in the bottom left and select the extension file you downloaded in the previous step.

Import VSM extension

Finally, click on the Install button once again.

## Install VSM extension

[Optional] Set up Wine for effect compilation

Effect (shader) compilation requires access to DirectX, so it will not work natively on macOS systems, but it can be used through Wine. Here are instructions to get this working.

## Install brew
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
Install wine64:

brew install xquartz
brew install wine-stable
brew install p7zip wget
```

Create wine prefix:
```
wget -qO- https://raw.githubusercontent.com/MonoGame/MonoGame/master/Tools/MonoGame.Effect.Compiler/mgfxc_wine_setup.sh | bash
```
If you ever need to undo the script, simply delete the .winemonogame folder in your home directory.



If you prefer to use JetBrains Rider or Visual Studio Code, after installing any of them you will need to install the .NET 6 SDK.

Once the .NET 6 SDK is installed, you can open a terminal and install the MonoGame templates by typing the following command:

```
dotnet new --install MonoGame.Templates.CSharp
```
Next up: Creating a new project







## Quick Start: Unix

Prerequisites for Linux:

Git
g++ >= 6
Prerequisites for macOS:

Apple Developer Tools
First, download and bootstrap vcpkg itself; it can be installed anywhere, but generally we recommend using vcpkg as a submodule for CMake projects.

```
$ git clone https://github.com/microsoft/vcpkg
$ ./vcpkg/bootstrap-vcpkg.sh
To install the libraries for your project, run:

$ ./vcpkg/vcpkg install [packages to install]
You can also search for the libraries you need with the search subcommand:

$ ./vcpkg/vcpkg search [search term]
In order to use vcpkg with CMake, you can use the toolchain file:

$ cmake -B [build directory] -S . "-DCMAKE_TOOLCHAIN_FILE=[path to vcpkg]/scripts/buildsystems/vcpkg.cmake"
$ cmake --build [build directory]
```
With CMake, you will still need to find_package and the like to use the libraries. Check out the CMake section for more information on how best to use vcpkg with CMake, and CMake Tools for VSCode.

Installing Linux Developer Tools
Across the different distros of Linux, there are different packages you'll need to install:

Debian, Ubuntu, popOS, and other Debian-based distributions:
$ sudo apt-get update
$ sudo apt-get install build-essential tar curl zip unzip
CentOS
$ sudo yum install centos-release-scl
$ sudo yum install devtoolset-7
$ scl enable devtoolset-7 bash
For any other distributions, make sure you're installing g++ 6 or above. If you want to add instructions for your specific distro, please open a PR!

Installing macOS Developer Tools
On macOS, the only thing you should need to do is run the following in your terminal:

$ xcode-select --install
Then follow along with the prompts in the windows that comes up.

You'll then be able to bootstrap vcpkg along with the quick start guide

Using vcpkg with CMake
Visual Studio Code with CMake Tools
Adding the following to your workspace settings.json will make CMake Tools automatically use vcpkg for libraries:

{
  "cmake.configureSettings": {
    "CMAKE_TOOLCHAIN_FILE": "[vcpkg root]/scripts/buildsystems/vcpkg.cmake"
  }
}
Vcpkg with Visual Studio CMake Projects
Open the CMake Settings Editor, and under CMake toolchain file, add the path to the vcpkg toolchain file:

[vcpkg root]/scripts/buildsystems/vcpkg.cmake
Vcpkg with CLion
Open the Toolchains settings (File > Settings on Windows and Linux, CLion > Preferences on macOS), and go to the CMake settings (Build, Execution, Deployment > CMake). Finally, in CMake options, add the following line:

-DCMAKE_TOOLCHAIN_FILE=[vcpkg root]/scripts/buildsystems/vcpkg.cmake
You must add this line to each profile.

Vcpkg as a Submodule
When using vcpkg as a submodule of your project, you can add the following to your CMakeLists.txt before the first project() call, instead of passing CMAKE_TOOLCHAIN_FILE to the cmake invocation.

set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake"
  CACHE STRING "Vcpkg toolchain file")
This will still allow people to not use vcpkg, by passing the CMAKE_TOOLCHAIN_FILE directly, but it will make the configure-build step slightly easier.

Tab-Completion/Auto-Completion
vcpkg supports auto-completion of commands, package names, and options in both powershell and bash. To enable tab-completion in the shell of your choice, run:

> .\vcpkg integrate powershell
or

$ ./vcpkg integrate bash # or zsh
depending on the shell you use, then restart your console.

Examples
See the documentation for specific walkthroughs, including installing and using a package, adding a new package from a zipfile, and adding a new package from a GitHub repo.

Our docs are now also available online at our website https://vcpkg.io/. We really appreciate any and all feedback! You can submit an issue in https://github.com/vcpkg/vcpkg.github.io/issues.

See a 4 minute video demo.

