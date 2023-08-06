# SSH

## Starting an ssh-agent on a remote host

(Using fish):

```
systemctl start ssh-agent --user
set -xg SSH_AUTH_SOCK "$XDG_RUNTIME_DIR/ssh-agent.socket"
```
