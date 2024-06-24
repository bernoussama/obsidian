Nix install plan (v0.19.0)
Planner: linux

Configured settings:
* diagnostic_endpoint: "https://install.determinate.systems/nix/diagnostic"
* extra_conf: []
* force: false
* init: "Systemd"
* modify_profile: true
* nix_build_group_id: 30000
* nix_build_group_name: "nixbld"
* nix_build_user_count: 32
* nix_build_user_id_base: 30000
* nix_build_user_prefix: "nixbld"
* nix_package_url: null
* proxy: null
* ssl_cert_file: null
* start_daemon: true

Planned actions:
* Extract the bundled Nix (originally from /nix/store/k51vv8b59cbjgf61l1klx6lqsa8mb0s1-nix-binary-tarball-2.21.2/nix-2.21.2-x86_64-linux.tar.xz)
* Create a directory tree in `/nix`
  Create directory `/nix/var/nix/userpool`
  Create directory `/nix/var/nix/daemon-socket`
* Move the downloaded Nix into `/nix`
  Nix is being downloaded to `/nix/temp-install-dir` and should be in `/nix`
* Create build users (UID 30001-30032) and group (GID 30000)
  The Nix daemon requires system users (and a group they share) which it can act as in order to build
  Create group `nixbld` (GID 30000)
  Create user `nixbld1` (UID 30001) in group `nixbld` (GID 30000)
  Create user `nixbld2` (UID 30002) in group `nixbld` (GID 30000)
  Create user `nixbld3` (UID 30003) in group `nixbld` (GID 30000)
  Create user `nixbld4` (UID 30004) in group `nixbld` (GID 30000)
  Create user `nixbld5` (UID 30005) in group `nixbld` (GID 30000)
  Create user `nixbld6` (UID 30006) in group `nixbld` (GID 30000)
  Create user `nixbld7` (UID 30007) in group `nixbld` (GID 30000)
  Create user `nixbld8` (UID 30008) in group `nixbld` (GID 30000)
  Create user `nixbld9` (UID 30009) in group `nixbld` (GID 30000)
  Create user `nixbld10` (UID 30010) in group `nixbld` (GID 30000)
  Create user `nixbld11` (UID 30011) in group `nixbld` (GID 30000)
  Create user `nixbld12` (UID 30012) in group `nixbld` (GID 30000)
  Create user `nixbld13` (UID 30013) in group `nixbld` (GID 30000)
  Create user `nixbld14` (UID 30014) in group `nixbld` (GID 30000)
  Create user `nixbld15` (UID 30015) in group `nixbld` (GID 30000)
  Create user `nixbld16` (UID 30016) in group `nixbld` (GID 30000)
  Create user `nixbld17` (UID 30017) in group `nixbld` (GID 30000)
  Create user `nixbld18` (UID 30018) in group `nixbld` (GID 30000)
  Create user `nixbld19` (UID 30019) in group `nixbld` (GID 30000)
  Create user `nixbld20` (UID 30020) in group `nixbld` (GID 30000)
  Create user `nixbld21` (UID 30021) in group `nixbld` (GID 30000)
  Create user `nixbld22` (UID 30022) in group `nixbld` (GID 30000)
  Create user `nixbld23` (UID 30023) in group `nixbld` (GID 30000)
  Create user `nixbld24` (UID 30024) in group `nixbld` (GID 30000)
  Create user `nixbld25` (UID 30025) in group `nixbld` (GID 30000)
  Create user `nixbld26` (UID 30026) in group `nixbld` (GID 30000)
  Create user `nixbld27` (UID 30027) in group `nixbld` (GID 30000)
  Create user `nixbld28` (UID 30028) in group `nixbld` (GID 30000)
  Create user `nixbld29` (UID 30029) in group `nixbld` (GID 30000)
  Create user `nixbld30` (UID 30030) in group `nixbld` (GID 30000)
  Create user `nixbld31` (UID 30031) in group `nixbld` (GID 30000)
  Create user `nixbld32` (UID 30032) in group `nixbld` (GID 30000)
  Add user `nixbld1` (UID 30001) to group `nixbld` (GID 30000)
  Add user `nixbld2` (UID 30002) to group `nixbld` (GID 30000)
  Add user `nixbld3` (UID 30003) to group `nixbld` (GID 30000)
  Add user `nixbld4` (UID 30004) to group `nixbld` (GID 30000)
  Add user `nixbld5` (UID 30005) to group `nixbld` (GID 30000)
  Add user `nixbld6` (UID 30006) to group `nixbld` (GID 30000)
  Add user `nixbld7` (UID 30007) to group `nixbld` (GID 30000)
  Add user `nixbld8` (UID 30008) to group `nixbld` (GID 30000)
  Add user `nixbld9` (UID 30009) to group `nixbld` (GID 30000)
  Add user `nixbld10` (UID 30010) to group `nixbld` (GID 30000)
  Add user `nixbld11` (UID 30011) to group `nixbld` (GID 30000)
  Add user `nixbld12` (UID 30012) to group `nixbld` (GID 30000)
  Add user `nixbld13` (UID 30013) to group `nixbld` (GID 30000)
  Add user `nixbld14` (UID 30014) to group `nixbld` (GID 30000)
  Add user `nixbld15` (UID 30015) to group `nixbld` (GID 30000)
  Add user `nixbld16` (UID 30016) to group `nixbld` (GID 30000)
  Add user `nixbld17` (UID 30017) to group `nixbld` (GID 30000)
  Add user `nixbld18` (UID 30018) to group `nixbld` (GID 30000)
  Add user `nixbld19` (UID 30019) to group `nixbld` (GID 30000)
  Add user `nixbld20` (UID 30020) to group `nixbld` (GID 30000)
  Add user `nixbld21` (UID 30021) to group `nixbld` (GID 30000)
  Add user `nixbld22` (UID 30022) to group `nixbld` (GID 30000)
  Add user `nixbld23` (UID 30023) to group `nixbld` (GID 30000)
  Add user `nixbld24` (UID 30024) to group `nixbld` (GID 30000)
  Add user `nixbld25` (UID 30025) to group `nixbld` (GID 30000)
  Add user `nixbld26` (UID 30026) to group `nixbld` (GID 30000)
  Add user `nixbld27` (UID 30027) to group `nixbld` (GID 30000)
  Add user `nixbld28` (UID 30028) to group `nixbld` (GID 30000)
  Add user `nixbld29` (UID 30029) to group `nixbld` (GID 30000)
  Add user `nixbld30` (UID 30030) to group `nixbld` (GID 30000)
  Add user `nixbld31` (UID 30031) to group `nixbld` (GID 30000)
  Add user `nixbld32` (UID 30032) to group `nixbld` (GID 30000)
* Setup the default Nix profile
* Place the Nix configuration in `/etc/nix/nix.conf`
  This file is read by the Nix daemon to set its configuration options at runtime.
  Create directory `/etc/nix`
  Merge or create nix.conf file `/etc/nix/nix.conf`
* Configure the shell profiles
  Update shell profiles to import Nix
* Configure Nix daemon related settings with systemd
  Run `systemd-tmpfiles --create --prefix=/nix/var/nix`
  Symlink `/nix/var/nix/profiles/default/lib/systemd/system/nix-daemon.service` to `/etc/systemd/system/nix-daemon.service`
  Symlink `/nix/var/nix/profiles/default/lib/systemd/system/nix-daemon.socket` to `/etc/systemd/system/nix-daemon.socket`
  Run `systemctl daemon-reload`
  Run `systemctl enable --now /nix/var/nix/profiles/default/lib/systemd/system/nix-daemon.socket`
* Remove directory `/nix/temp-install-dir`

