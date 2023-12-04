# Add a Build

### 1. Your First Build

Builds in Elixir Platform are used for version control. Every new Build represents a new version of the Game. Creating a build is a simple task:

* Choose your own version naming
* Have control of which build you have active to perform new releases and rollbacks

![](<../../../.gitbook/assets/Screenshot 2022-08-15 at 19.22.54.png>)

Do not forget to activate the Build once everything is ready. Also, you can always de-activate it when you want to close the access to the game. Or perform a roll-back by activating older builds just by using the toggles:

![](<../../../.gitbook/assets/Screenshot 2022-08-15 at 19.24.01.png>)

### 2. Your First Depot

Now that you have created a Game Build. Let upload the file so you can start playing it. For this you will need to configure the Depot: A configuration file that will include information about the Game File and how to execute it.

* **Installation Path**: Do not modify this path. We are planning on removing it from here for the next version.
* **Launch Command**: It should follow a structure like `"<InstallationPath>/<route to the executable file>".` See [Recommendations](add-a-build.md#recommendations-and-usual-errors)

