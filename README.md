## Easy mass execute command or script on list of hosts

Execute ssh command or bash script sequentally over list of hosts.

### Usage

    mh [hosts specificatior] [options] [command...]

**Host specificator** is:

- `:abc:` - hosts with tag `abc`.
- `:abc`  - hosts where tag starts with `abc`.
- `/RE/`  - hosts which match regular expression.

All above commands select hosts from file `~/.mh`. Format of `~/.mh` file is - first column is host name (and tag), other columns are (just) tags. If you need to specify connection options for hosts, like ssh port, please specify them in `~/.ssh/config`.

- `@abc,def @ghi user@xyz`- manually specify hosts w/o using `.mh` file.

If you don't specify _command_ `mh` will just print selected hosts.

**Options** are:

- `--list` list selected hosts and exit, w/o running command.
- `-H` suppress hosts prefix in output.
- `--vz` execute command also in OpenVZ containers on targets using `vzctl exec`.
- `--vz=RE` to select only containers where hostname matches RE.
- `--script=file` execute script `file` on remotes.
- `--edit=file` execute script but first run editor over it, if file does not exist it will be created.
- `--edit` will edit temporary file, execute, and delete it.
- `--` end of options separator.
- `command...` any command as in ssh. When both script and command are used, script will be executed first.

**Tips**:

- Ssh command on two hosts: `mh @hosta @hostb uname -a` or `mh @hosta,hostb uname -a`.

- To execute several commands use `--edit=` option with meaningful script name: `mh :web: --edit=install-xyz`. No `install-xyz` is required to exists before run. Second run will edit the same file, so it's useful if you made mistake first time. If you don't need to run editor change command to `mh :web: --script=install-xyz`.

