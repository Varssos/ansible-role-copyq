# copyq

Ansible role to install [CopyQ](https://hluk.github.io/CopyQ/) clipboard manager and configure a global tray shortcut on Debian/Ubuntu systems.

## Requirements

- Debian or Ubuntu host
- `become: true` privileges (sudo)
- GUI/X11 session required at runtime for shortcut configuration (skipped gracefully in VMs)

## Role Variables

| Variable | Default | Description |
|---|---|---|
| `copyq_package_name` | `copyq` | Package name to install via apt |
| `copyq_tray_shortcut` | `ctrl+shift+v` | Global shortcut for the tray menu |

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - role: copyq
```

## Manual setup (without Ansible)

Install CopyQ, then run its configuration commands as your desktop user in
an active graphical session (not with sudo):

```bash
sudo apt install copyq
copyq --start-server
copyq eval '
  var cmds = commands();
  var found = false;
  for (var index in cmds) {
    if (cmds[index].name === "Show the tray menu") {
      cmds[index].cmd = "copyq menu";
      cmds[index].shortcuts = ["ctrl+shift+v"];
      cmds[index].globalShortcuts = ["ctrl+shift+v"];
      cmds[index].isGlobalShortcut = true;
      cmds[index].enable = true;
      found = true;
      break;
    }
  }
  if (!found) {
    cmds.push({name: "Show the tray menu", cmd: "copyq menu",
      shortcuts: ["ctrl+shift+v"], globalShortcuts: ["ctrl+shift+v"],
      isGlobalShortcut: true, enable: true});
  }
  setCommands(cmds);
'
```

## License

MIT

## Author

Varssos