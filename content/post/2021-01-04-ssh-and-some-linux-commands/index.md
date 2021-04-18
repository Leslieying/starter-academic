---
title: SSH and Some Linux Commands
author: Rui Ying
date: '2021-01-04'
slug: []
categories:
  - Linux
  - SSH
tags: []
---
# What's public key and private key (in my understanding)
Public key and private key are generated pairwisely. Only each other can decode the other. One of the pair can be the lock and the other can be the key.

# SSH connection process

- Client sends a request
- Server receives the request and send pub_key to client
- client uses the pub_key to encrypt password and send back
- Server decodes it using private_key
*Core*: use server's public key to encrypt user's password.

# SSH connection without typing passwords

- Client generate public and private key of itself, and store the public one in server local
- Server send a random string to client
- Client uses its private key to encrypt the random string
- Server try to use public key to decode

*Core*:  compare client's public and private key without typing passwords
It's equal to
```bash
ssh user@host 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
```
Then I went to search the linux commands...

## How to generate ssh key on client PC and store in server
```bash
ssh-keygen; ssh-copy-id user@host
```

# New-learned Linux commands


|Command|Description|
|--|--|
|>|redirect output (rewriting)|
| >>|redirect output (append)|
|<|redirect input to command|
|&&| logic "AND", or "if success then:"|
|\|\||logic "OR"|
|;|like the ";" in C or Java|
|sort| ranking something|

# Redirect example command
```bash
2>&1 #is equal to &>
```
What's the number represents?
0 -> stdin
1 -> stdout
2 -> stderr

Because `1` is the default, so `1>` is equivalent to `>`. The `2>&1` means add stderr to stdout

[Example from stackoverflow](https://stackoverflow.com/questions/818255/in-the-shell-what-does-21-mean)
```bash
echo test 1> afile.txt #redirect stdout
echo test 2> afile.txt #redirect stderr (which is the bad result: warnings)
echo test 1>&2 afile.txt #redirect both
```
What about both `<` and `>` appear? We usually have input first, output second, so command receive `<` then `>` output.
e.g. `cat > output.txt < input.txt`
