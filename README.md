# connect_spice
A simple shell script which servers as a wrapper for `spice-example-sh` that connects to a Proxmox VM via SPICE.

This repository also includes that script, with some minor alterations to remove some redundant code. You can find the original [here.](https://git.proxmox.com/?p=pve-manager.git;a=blob_plain;f=spice-example-sh;hb=HEAD)

## Usage

You obviously need a running VM on your hypervisor with a suitable SPICE display adapter. You'll also need virt-viewer for your distribution.

I have a directory `~/scripts` in which I keep various utility scripts I have written, this directory is also within my `$PATH` within my `~/.bashrc` so I can invoke the scripts from anywhere.

Clone the repository in this directory —

```bash
git clone https://www.github.com/dwhweb/connect_spice.git
```

Once you've done that, the general usage pattern is to copy `connect_spice` and `connect_spice.yml` with whatever name you want, for example `connect_mybox` and `connect_mybox.yml`. The associated config file for the script should always use the same name as the script with a `.yml` extension.

The config YAML file can contain the following key-value pairs —

* `username`
* `password`
* `node_number` — The number of the VM you want to connect to
* `cluster_hostname` — The hostname for the cluster you want to connect to (IP addresses don't work due to the way the underlying API operates)
* `proxy` — Hostname or address of the pveproxy (Proxmox REST API)

If the associated config file is missing or any of these key-value pairs are missing you will be interactively prompted for the value, with the exception of the value for `proxy`. If this is missing, then is is assumed that pveproxy is running on the same machine as the host cluster you are trying to connect to (the value of `cluster_hostname`), which is true in most cases.

I'd probably advise you omit the password from the config to prevent storing credentials in plaintext on the disk, but the option is there if you need it. It's probably a good idea to change the permissions on any config files to 600 regardless.

Once you're happy with this, you'll probably want to symlink the script in `~/scripts`, e.g.

```bash
ln -s ~/scripts/connect_spice/connect_mybox connect_mybox.sh
```

Then invoke whenever you want to connect to the box.

## Licence

The script is written by dwhweb, and distributed under the terms of the AGPL (the same terms as the script it wraps).
