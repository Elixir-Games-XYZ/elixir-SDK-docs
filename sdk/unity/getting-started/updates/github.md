# GitHub

{% hint style="info" %}
&#x20;Elixir SDK for Unity is available at [https://github.com/Elixir-Games-XYZ/elixir-unity-sdk](https://github.com/Elixir-Games-XYZ/elixir-unity-sdk)
{% endhint %}

## Existing Git Repositories

This workflow is for games that use `git` as their primary version control system.

### Getting Started

If you are already using `git` as the version control system of choice for your game, you will need to add `ElixirUnitySDK` as a git submodule.

1. Navigate to the `Assets` directory in your game
2. Run:\
   `git submodule add git@github.com:Elixir-Games-XYZ/elixir-unity-sdk.git ElixirUnitySDK`
3. Verify that a file named `.gitmodule` appeared at the root of your game project folder, and that the Elixir SDK for Unity has been correctly pulled into `Assets/ElixirUnitySDK`
4. This change will now be staged for a commit. Commit it by running `git commit` with a message. For example: \
   `git commit -m "Feat: Added Elixir SDK"`

### Cloning

{% hint style="warning" %}
If you do not do this when you clone your game's repository, the submodule will not be correctly initialized
{% endhint %}

Working with git submodules introduces one extra step when cloning your repository on a new machine.

1. Clone your game as usual: \
   `git clone YOUR_GIT_REPO`
2. **NEW STEP:** Initialize the submodules by running: \
   `git submodule update --init --recursive`

### **Pulling**

{% hint style="warning" %}
If you do not pull changes from your repository correctly , the submodule will not be updated
{% endhint %}

To pull in all changes in your repository including changes in submodules you can run:

```bash
git pull --recurse-submodules
```

### Updating Submodule

To fetch the latest changes from the Elixir SDK repository run the following:

```bash
git submodule update --remote
```

You will then be required to commit this change in order to persist the commit of the submodule that your game's repository is pointing to.
