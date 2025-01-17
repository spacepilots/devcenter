---
tag: []
title: Adding an app from the CLI
redirect_from: []
summary: ''
published: false

---
You can easily register a new Bitrise app from the Bitrise CLI: the process is guided and simple to follow.

You have all the options that are available on the Bitrise website:

* You can choose the account that will own the app.
* You can add private and public apps.
* The scanner can automatically detect the type of your app, or you can configure it manually. 
* You can register an SSH key automatically or manually. 

{% include message_box.html type="note" title="Adding an app with the API" content="You can also use the Bitrise API to add a new app. To do so, check out our [Adding and managing apps](/api/adding-and-managing-apps/) guide."%}

## Before you start

Before you try adding a new app to Bitrise via our CLI, make sure a few things are in order:

* You need a Bitrise account, with a connected git provider.
* You need the Bitrise CLI: check out our [Installing and updating the Bitrise CLI](/bitrise-cli/installation/) guide.
* Your project must have a local Git repository on your machine and a remote repository at a Git provider. If you want to use an SSH key to access the repository, [the remote repository URL must be an SSH URL](https://help.github.com/en/articles/which-remote-url-should-i-use)! For example, `git@github.com/example.git`.
* You need a personal access token: check out our [Generating personal access tokens manually](https://devcenter.bitrise.io/getting-started/account-security/#generating-personal-access-tokens-manually) guide.

You can also create a bitrise.yml in advance and add it to the repository. The scanner will automatically detect it and you can use it for your app. 

## Adding a new app from the CLI

This procedure guides you through adding an app which Bitrise will access with an SSH key. This requires that the app's remote repository has an SSH URL, such as `git@github.com:example-user/example.git`.

You can, of course, use an HTTPS URL to access your remote repository, too: in that case, you will not set an SSH key for your app. Everything else in the process is the same. 

1. Open a command line interface.
2. Go to the location of your project. 
3. Run the below command, with your personal access token replacing the placeholder:
   ```
   bitrise-add-new-project --api-token <YOUR PERSONAL ACCESS TOKEN>
   ```
4. Use the arrow keys to the account that will be the owner of the app and press Enter. 
   ```
   ? Select account to use
     > Example-person
       Example-org
   ```
5. Select the privacy of the app and press Enter. 
   You can add either a private or a public app.
   ```
   ? Select privacy:
    > Private
      Public
   ```
   Once you are done, the scanner will scan your repository and look for the remote repository's URL. 
6. Select the repository URL: choose the SSH option. 
   This step only comes up if your local repository's remote has an SSH URL. If the remote repository has an HTTPS URL, you won't see this prompt. 
   ``` 
   Remote URL: git@github.com:example-user/example.git
   
   ? Select repository URL::
       https://github.com/example-user/example.git
     > ssh://git@github.com:example-user/example.git
   ```
6. Register an SSH key.
   ```
    Specify how Bitrise will be able to access the source code: 
    > Automatic
      Add own SSH
   ```
   You can select either the automatic registration or choose to add your own. 
   * If you choose automatic, Bitrise will automatically generate a key pair. If you need to use additional private repositories or submodules, choose the `I need to` option when prompted and follow the instructions. If not, select the `No, auto-add SSH key` option: this automatically adds the public key to your repository.
   * If you choose to add your own, you have to provide the file path to both the private and the public key file. Alternatively, you can drag and drop the files to the CLI. 
6. Decide what bitrise.yml do you want to upload.
   ```  
   ? What bitrise.yml do you want to upload? 
     > Run the scanner to generate a new bitrise.yml
       Use an already existing bitrise.yml
   ```
   If you have an existing `bitrise.yml` file in your repository, the second option tells Bitrise to use that. If you do not have an existing `bitrise.yml`, you can either have the scanner generate one based on your project files or you can provide a file, either by entering its path or dragging and dropping it to the CLI. 
7. Select the branch you want to use. 
   The default option is the current active branch. 
   ```
   The current branch is: master (tracking: origin master),
   
   ? Do you want to run the scanner for this branch?
     > Yes
       No
   ```
 