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

## License

MIT

## Author

Varssos