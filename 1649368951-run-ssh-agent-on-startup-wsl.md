# 1649368951 run-ssh-agent-on-startup-wsl

Sometimes we need to run ssh-agent on startup for wsl.
AFAIK, there is bug when we restart wsl2 ssh-agent does not spin up

This solution will work not only for wsl but for usual Linux as well

Add following **./bashrc** or **./zshrc**
```shell
if [ -z "$(pgrep ssh-agent)" ]; then
   rm -rf /tmp/ssh-*
   eval $(ssh-agent -s) > /dev/null
else
   export SSH_AGENT_PID=$(pgrep ssh-agent)
   export SSH_AUTH_SOCK=$(find /tmp/ssh-* -name agent.*)
fi
```


## Links
