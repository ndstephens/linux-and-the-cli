# SSH - Secure Shell

**_I have some great articles bookmarked regarding SSH and how to create and configure them_**

- Many times the only real way to administrate and run code on a cloud server is to connect into a remote CLI session and run the code yourself.
- When you generate a new `ssh` key, you get two files, a `public key` and a `private key`.
  - The `public key` is what you give to everyone else and is not a secret.
    - You're basically giving them a key hole and telling them to install it on a door for you.
  - The `private key` should never be revealed to anyone.
    - If anyone does get ahold of this key they can freely masquerade as you. This is the key to the key hole.
    - If you do accidentally reveal your `private key` ever, you should immediately delete your `public key` in all locations it exists and create new keys.

## Create an SSH key

```sh
ssh-keygen -t rsa <or-other-hash-algorithm>
# hit enter to put the key files in the default place OR enter another location
# hit enter to give an empty passphrase OR enter a passphrase
# hit enter again to confirm
```

> The two main hash algorithms are `ed25519` and `rsa`.
>
> Here we're generating a new random key. This key is essentially unguessable and un-hackable from a brute-force perspective.
>
> Put keys in the `~/.ssh` directory, which is standard.
>
> In general it's a good idea to give it a passphrase so that anytime you use the SSH key you need to enter a passphrase (and frequently you can save a passphrase to something like macOS's `keychain`).
>
> The passphrase helps keep you safe if the `private key` is exposed.

- If you run `ls ~/.ssh` you'll at least see `id_rsa` (your private key) and `id_rsa.pub` (your public key).

## Provide remote machine with your public key

- With services like Azure or DigitalOcean, you'll usually give them your `id_rsa.pub` and they'll take care of making sure it gets into `authorized_keys`.
- Hypothetical example of manually adding it to a remote machine:
  - Locally, run `cat ~/.ssh/id_rsa.pub` and copy the output onto your clipboard
  - On the remote machine:

```sh
su <remote-user-account>
mkdir ~/.ssh
vi ~/.ssh/authorized_keys # paste in copied ssh id_rsa.pub from local, then write and quit
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

## Connect to remote via SSH

- Need to give `ssh` an address to connect to.
- You need the remote username and the remote IP address (or domain) to tell your computer where to connect to.

```sh
ssh <remote-user-account>@<remote-ip-address-or-domain>
```

- Now you can remotely connect to your server in the cloud or your Raspberry Pi in the other room.
- It works with any Linux machine you can connect to over the network.
