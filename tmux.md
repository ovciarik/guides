- Create new session
```bash
tmux
```
```bash
tmux new -s session_name
```

- List sessions
```bash
tmux ls
```

- Attach running session
```bash
tmux a 
```
```bash
tmux a -t session_name
```

- Detach session
```bash
^b d
```

- Kill session (from inside of tmux)
```bash
^d
```
- Kill session (from shell)
```bash
tmux kill-session -t session_name
```

---

- Create new window
```bash
^b c
```

- Select window 1
```bash
^b 1
```

- Select window 2
```bash
^b 2
```

- Delete window
```bash
^b x
```
