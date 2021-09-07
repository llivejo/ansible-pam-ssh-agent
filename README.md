# ansible-pam-ssh-agent

Ansible playbook to setup `libpam-ssh-agent-auth` for sudo authentication via forwarded ssh-agent  socket.

After running this playbook on a Debian/Ubuntu host you will be able to use `sudo` without entering your password: you will be authorized by SSH key in your local SSH-agent only.

Advantages:
 - no more passwords
 - SSH key never leaves your local machine
 - attacker with your user's privileges cannot gain root (at least without _active_ SSH connection and unlocked ssh-agent on your machine)
 - you still can use your password for sudo when ssh-agent forwarding is not available
 - no more insecure NOPASSWD in `/etc/sudoers`

Disadvantages:
 - you have to enable ssh-agent forwarding to remote host which might increase overall attack surface

## Usage
`ansible-playbook -i myservers -v -K install-libpam-ssh-agent.yml`

`-K` needed for your password for sudo on remote host (this will be the last time you enter it!)

## Modified files
`/etc/sudoers` (in case there is NOPASSWD in it)
`/etc/pam.d/sudo`
