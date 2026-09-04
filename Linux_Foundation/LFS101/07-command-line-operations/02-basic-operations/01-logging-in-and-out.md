# Logging In and Out (Command Line)

## 1. Logging In at a Text Terminal

An available text terminal prompts for a username (the `login:` string) and password.

> [!NOTE]
> While typing the password, nothing is displayed on the terminal — not even a `*` — to prevent others from seeing it. This is expected behavior, not a stuck terminal.

Once logged in, either at a text terminal or through a graphical terminal program, standard command-line operations become available.

## 2. Connecting to Remote Systems with SSH

**SSH** (Secure SHell) connects and logs into a remote system securely from the current session:

```bash
$ ssh student@remote-server.com
```

This connects securely to `remote-server.com` and gives the `student` account a command-line terminal on that machine, authenticated with either a password (as with a regular login) or a cryptographic key that signs in without requiring a password.

> [!NOTE]
> The first time you connect to a given remote host, SSH shows its **host key fingerprint** and asks for confirmation before continuing. Accepting it records the key locally, so future connections to that same host are verified automatically, and any unexpected change is flagged — a basic safeguard against connecting to an impostor server.
