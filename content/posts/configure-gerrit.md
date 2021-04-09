# \# Configuring Gerrit

## \## Generating SSH Key

```bash
cd ~/
ssh-keygen -t rsa
```

After that it will ask for the key location, for default press enter.

Then it will ask you to add password, for blank pass press enter.

**[Note: If u want to add any password you can do it, that password is always required when you push commits]**

## \## Setting up gerrit account

Open the gerrit you want to configure and Sign-up with ur github. After successful sign-up go to `http://<gerrit_link>/#/settings/contact` and register ur email, and then go to `http://<gerrit_link>/#/settings`, make sure every information is filled up correctly.

```text
1. Username       xxxxxx
2. Full Name      xxxxxx
3. Email Address  xxxxxx@xxxx.com
4. Registered     xxxxx xx:xx
5. Account ID     100xxxx
```

## \## Adding SSH Key to gerrit

Open your terminal and type:

```bash
cat .ssh/id_rsa.pub
```

Copy the SSH key and paste it on `http://<gerrit_link>/#/settings/ssh-keys` and save it.

## \## Creating config file

First type:

`$ nano .ssh/config`

And add these details there:

```text
Host <gerrit_link>
HostName <gerrit_link>
Port 29418
User <YourGerritUsername>
```

Save and exit the file after doing so.

## \## Granting required permissions

Type the following commands:

```bash
chmod 600 .ssh/config
chmod 700 .ssh/
chmod 600 .ssh/id_rsa
```

## \## Checking everything

To check everything is fine, do a connection Test by typing -> `ssh <gerrit_link>` [Type yes if they ask for it]

```text
               Welcome to Gerrit Code Review

Hi <YourGerritUserName>, you have successfully connected over SSH.

Unfortunately, interactive shells are disabled.
To clone a hosted Git repository, use:

git clone ssh://<YourGerritUserName>@<gerrit_link>:29418/REPOSITORY_NAME.git

Connection to <gerrit_link> closed.
```

**[If you get the above output message, your gerrit is configured]**

## \## Pushing changes to gerrit

Commit all required changes you need to push and use the below command to add hook to it:

```bash
gitdir=$(git rev-parse --git-dir); scp -p -P 29418 <YourGerritUsername>@<gerrit_link>:hooks/commit-msg ${gitdir}/hooks/
```

Then use the following command to push:

```bash
git push ssh://<YourGerritUserName>@<gerrit_link>:29418/<ROM_NAME>/<REPOSITORY_NAME> HEAD:refs/for/<branchname>
```

**Everything is configured and you're good to go now!**
