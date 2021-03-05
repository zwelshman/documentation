## Running your code on the server

To run code for real in the production environment, use the [https://jobs.opensafely.org](https://jobs.opensafely.org) site.
Here you can see (even without a login) all the ongoing projects within OpenSAFELY, and the specific _jobs_ that have been run on the server.
To submit jobs (i.e., to run actions), the general process is as follows:

*  **Log in** using your GitHub credentials (this should happen automatically if you have access to the OpenSAFELY GitHub organisation).
* **Create a workspace** (or select an existing workspace):
	* click the `Add a New WorkSpace` button
	* choose a name, for example the name of the repo
	* select a database to run against (either dummy data, real data, or a small sample of the real data)
	* select the repo and branch that you want to run actions with
	* click `Submit`.
*  **Select actions** to run:
	* select the actions you want to run by clicking the `Run` buttons
	* if any of these actions have dependencies then they will also be run, unless their outputs already exist
	* dependencies can be viewed by clicking the `Needs` button
	* you can force dependencies to be run by clicking `Force run dependencies`, even if those actions have already been run
	* when you're ready, click `Submit`.

The workspace is available at `https://jobs.opensafely.org/<WORKSPACE_NAME>/`.
You can view the progress of these actions by click the `Logs` button from the workspace, or going to `https://jobs.opensafely.org/<WORKSPACE_NAME>/logs`.

<details markdown="1">
<summary>Click here for information on the exact steps that occur when each job is run on the server</summary>

What happens:

1. A new, empty temporary directory for the job is created
2. Copy in all files on the selected branch
3. The job is run
4. All the files matching the specified output patterns are copied into the local repo
5. The log files for the job are saved into the `metadata/` directory
6. The temporary directory is deleted
</details>

The job will either succeed or fail.
In either case, the output and log files are only visible in the secure environment to avoid disclosure of potentially sensitive information.