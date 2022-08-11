# Role Name

A brief description of the role goes here.

## Требования

Debian или Ubuntu

## Переменные

```yaml
nfs_foldes_create: true
nfs_foldes:
  - path: "/nfs/foo"
    address: "192.168.100.0/24"
    permissions: "(rw,sync,no_subtree_check)"
```

## Пример Playbook

```yaml
- hosts:
    - all

  vars:
    nfs_foldes_create: true
    nfs_foldes:
      - path: "/nfs/foo"
        address: "192.168.100.0/24"
        permissions: "(rw,sync,no_subtree_check)"
      - path: "/nfs/bar"
        address: "*"
        permissions: "(rw,sync,no_root_squash,no_subtree_check"

  roles:
    - role: imbicile.nfs
      become: true
```

### Локальная проверка

```bash
[root][debian-test][/nfs]
# mount -t nfs 127.0.0.1:/nfs/foo /mnt/
mount.nfs: access denied by server while mounting 127.0.0.1:/nfs/foo
[root][debian-test][/nfs]
# mount -t nfs 127.0.0.1:/nfs/bar /mnt/
[root][debian-test][/nfs]
#
```

### Порты для работы NFS

[SecuringNFS](https://wiki.debian.org/SecuringNFS)

```
 ACCEPT          fw      loc             udp     111
 ACCEPT          fw      loc             tcp     111
 ACCEPT          fw      loc             tcp     2049
 ACCEPT          fw      loc             udp     2049
 ACCEPT          fw      loc             tcp     32764:32769
 ACCEPT          fw      loc             udp     32764:32769
```
