# The fix

The issue is the hardcoded admin password. The fix is to use a placeholder that gets replaced with the password
during runtime. 

I replaced the hardcoded password with a placeholder - ADMIN_PASSWORD. Now with environment variables we can set the admin password. 
We **should not** reuse the password that we removed, because it is now in git history and anyone with repo access 
can see it.

Instead we should generate a secure password and use it. If ADMIN_PASSWORD isn't set then application will fail fast, 
indicating that something is not right with the application's configuration, in this case, the password.


Intellij usage: Set the environment variable ADMIN_PASSWORD in run configuration.
Docker usage: Set the environment variable ADMIN_PASSWORD in the run command (check readme), by adding `-e ADMIN_PASSWORD=your_password`

Ideally, docker command should get the secret from some secret manager, for example it will be run from github actions,
then secret should be in github actions secret store.
