# 020 - GitHub Authentication

GitHub requires authentication for write operations, so we will be **prompted for our user account name and a token for every *push* operation**.

## Step 1: Create the Token (PAT)

There are several types of GitHub tokens, but we will use the **Personal access tokens (PAT, classic)**. Let's follow the GitHub documentation to create the token:

https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-personal-access-token-classic

## Step 2: Use the Token in the Terminal

We will use the built-in features of Git to cache the GitHub PAT token &rarr; **In-Memory Cache (Most Secure)**

This **temporarily stores your token in memory and never writes it to your hard drive**. By default, it forgets the token after 15 minutes, but you can customize the timeout:

```bash
$ git config --global credential.helper 'cache --timeout=7200' # keep cached for 2 hours
```