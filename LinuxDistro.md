# Linux Distro Ideas

Ideas for a lightweight linux distro with a lot of rust and a focus on performance, security, and ease of use.

**Release**: Rolling with optimized packages similiar to CachyOS
**Package Manager**: [Redox's pkg](https://github.com/redox-os/pkgutils)
**Immutable**: Maybe
**Installer**: [Pop!_OS Installer](https://github.com/pop-os/installer?tab=readme-ov-file)

### Features

- Offer full disk encryption with luks2 on install
  - Maybe have useful tool for updating drives in fstab and boot parameters when using encryption
- Secure Boot 
  - availible on install if possible (I think fedora can do this)
  - easily enabled after first boot
  - w/ machine owner key or optionally with shim
- Generate initramfs with [booster](https://github.com/anatol/booster)
- Maybe use [blsforme](https://github.com/AerynOS/blsforme?tab=readme-ov-file)
- Use [refind](https://www.rodsbooks.com/refind/) for boot manager
  - Develop a custom theme
  - Use [refind-btrfs](https://github.com/Venom1991/refind-btrfs) for backup management
- Login with [greetd](https://git.sr.ht/~kennylevinsen/greetd)
  - [QtGreet](https://gitlab.com/marcusbritanicus/QtGreet)
  - [Cosmic Greeter](https://github.com/pop-os/cosmic-greeter)
- Come default with firewall rules and update with package installs
- Offer [stratis](https://github.com/stratis-storage/stratisd)
- Special install options for developers
  - Install groups of packages based on programming language
    - Maybe have a special group for web
  - Let users choose between podman and docker
- App store like [cosmic store](https://github.com/pop-os/cosmic-store) or [Pop!_Shop](https://github.com/pop-os/shop)
- Backups with [Pop!_OS Snapshot](https://github.com/pop-os/snapshot)

### Immutable

- [Transactional Updates](https://kubic.opensuse.org/documentation/transactional-update-guide/tu-introduction.html#tu-introduction-description)
- Blue/Green deployment with btrfs

### Packaging

I really like Redox's `pkg` but I also like AerynOS's [moss](https://github.com/AerynOS/os-tools)

- Should send packages with zstd compression

#### For later review

- [buildchain](https://github.com/pop-os/buildchain)
- [a piece of pisi](https://github.com/AerynOS/a-piece-of-pisi)
- [zenith](https://github.com/AerynOS/zenith)

### Pid 1

systemd, [s6](https://skarnet.org/software/s6/), [Open Euler's sysmaster](https://gitee.com/openeuler/sysmaster/blob/master/docs/en/sysmaster_usage.md).
- Systemd would be a lot easier for a lot of reasons
- S6 would be lighter
  - Would be fun (I think) to make something like [66](https://web.obarun.org/software/66/0.8.2.1/index/) in rust
- Sysmaster feels on brand for the goals of this project

### Shells

- Use nushell for default system shell
  - While I'd like to use binaries instead of a shell for most things I do think that nushell's structured data would make script maintenance easier
- Let user's pick from fish, zsh, and nushell

### CLI Tools

#### Default

- [3cpio](https://github.com/bdrung/3cpio):  manage initrd cpio archives 
- [atuin](https://github.com/ellie/atuin): "Magical shell history"
- [bat](https://github.com/sharkdp/bat): A replacement for `cat` that provides syntax highlighting and other features. 
- [bottom](https://github.com/ClementTsang/bottom): Yet another cross-platform graphical process/system monitor. 
- [broot](https://github.com/Canop/broot): A new way to see and navigate directory trees
- [bustd](https://github.com/vrmiguel/bustd): OOM 
- [coreutils](https://github.com/uutils/coreutils)
- [dust](https://github.com/bootandy/dust): "a more intuitive version of `du` in Rust"
- [eva](https://github.com/oppiliappan/eva):  a calculator REPL, similar to bc(1) 
- [eza](https://github.com/eza-community/eza): "A modern version of `ls`".
- [fd](https://github.com/sharkdp/fd): "A simple, fast and user-friendly alternative to `find`"
- [frawk](https://github.com/ezrosent/frawk):  an efficient awk-like language 
- [lfs](https://github.com/Canop/lfs): A Linux utility to get information on filesystems; like `df` but better 
- [hck](https://github.com/sstadick/hck): `cut` with decompression, column reordering and regex as delimiter
- [navi](https://github.com/denisidoro/navi):  An interactive cheatsheet tool for the command-line 
- [ntpd-rs](https://github.com/pendulum-project/ntpd-rs): A full-featured implementation of the Network Time Protocol, including NTS support. 
- [procs](https://github.com/dalance/procs): A modern replacement for `ps` written in Rust
- [rage](https://github.com/str4d/rage):  A simple, secure and modern file encryption tool (and Rust library) with small explicit keys, no config options, and UNIX-style composability. 
- [rargs](https://github.com/lotabout/rargs):  xargs + awk with pattern matching support. `ls *.bak | rargs -p '(.*)\.bak' mv {0} {1}` 
- [rink](https://github.com/tiffany352/rink-rs/):  Unit conversion tool and library written in rust 
- [rip](https://github.com/nivekuil/rip): A safe and ergonomic alternative to `rm`
- [ripgrep](https://github.com/BurntSushi/ripgrep): A faster replacement for GNU’s `grep` command. This tool is very good.
- [ripgrep-all](https://github.com/phiresky/ripgrep-all) to search PDFs, E-Books, Office documents, zip, tar.gz, etc.
- [rnr](https://github.com/ismaelgv/rnr): "A command-line tool to batch rename files and directories"
- [sad](https://github.com/ms-jpq/sad):  CLI search and replace | Space Age seD 
- [skim](https://github.com/lotabout/skim): A command-line fuzzy finder.
- [sudo-rs](https://github.com/trifectatechfoundation/sudo-rs):  A memory safe implementation of sudo and su. 
- [systeriod](https://github.com/orhun/systeroid):  A more powerful alternative to sysctl(8) with a terminal user interface 🐧 
- [tealdear](https://github.com/dbrgn/tealdeer): A very fast implementation of `tldr` in Rust. 
- [tokei](https://github.com/XAMPPRocky/tokei): Count your (lines of) code, quickly
- [starship](https://starship.rs/): Customizable prompt for any shell.
- [xcp](https://github.com/tarka/xcp): An extended `cp` 
- [zellij](https://github.com/zellij-org/zellij): A terminal workspace with batteries included.

#### Developer

- [bandwhich](https://github.com/imsnif/bandwhich): Terminal bandwidth utilization tool 
- [delta](https://github.com/dandavison/delta): A syntax-highlighting pager for git, `diff`, and grep output 
- [difftastic](https://github.com/Wilfred/difftastic/): A syntax-aware diff  
- [dog](https://github.com/ogham/dog): A command-line DNS client
- [fnm](https://github.com/Schniz/fnm):  🚀 Fast and simple Node.js version manager, built in Rust 
- [frum](https://github.com/TaKO8Ki/frum): A modern Ruby version manager written in Rust
- [gitoxide](https://github.com/GitoxideLabs/gitoxide)
- [gitui](https://github.com/gitui-org/gitui):  Blazing 💥 fast terminal-ui for git written in rust 🦀 
- [helix](https://github.com/helix-editor/helix):  A post-modern modal text editor. 
- [htmlq](https://github.com/mgdm/htmlq): Like jq, but for HTML. Uses CSS selectors to extract bits of content from HTML files.
- [hyperfine](https://github.com/sharkdp/hyperfine): Command-line benchmarking tool- tokei
- [jless](https://github.com/PaulJuliusMartinez/jless): "command-line JSON viewer designed for reading, exploring, and searching through JSON data."
- [jql](https://github.com/yamafaktory/jql): A JSON query language CLI tool
- [just](https://github.com/casey/just): Just a command runner (seems like an alternative to `make`)
- [pastel](https://github.com/sharkdp/pastel):  A command-line tool to generate, analyze, convert and manipulate colors 
- [ripsecrets](https://github.com/sirwart/ripsecrets): Find secret keys in your code before commiting them to git. I've contributed to this one!
- [ruff](https://github.com/astral-sh/ruff):  An extremely fast Python linter and code formatter, written in Rust. 
- [rustls-ffi](https://github.com/rustls/rustls-ffi): FFI bindings for the rustls TLS library, so you can use the library in any language that supports FFI (C, C++, Python, etc)
- [rutabaga_gfx](https://github.com/magma-gpu/rutabaga_gfx):  Cross-platform, open-source, Rust-based GPU paravirtualization 
- [selene](https://github.com/Kampfkarren/selene):  A blazing-fast modern Lua linter written in Rust 
- [step](https://github.com/smallstep/cli):  🧰 A zero trust swiss army knife for working with X509, OAuth, JWT, OATH OTP, etc. 
- [system76 power](https://github.com/pop-os/system76-power): A sophisticated power management daemon. It’s better than TLP for modern laptops.
- [uv](https://github.com/astral-sh/uv):  An extremely fast Python package and project manager, written in Rust. 
- [watchexec](https://github.com/watchexec/watchexec): Execute commands in response to file modifications.
- [wild](https://github.com/davidlattimore/wild):  A very fast linker for Linux 
- [xh](https://github.com/ducaale/xh): "Friendly and fast tool for sending HTTP requests" 

### Terminal

- [Alacritty](https://github.com/alacritty/alacritty): A cross-platform, OpenGL terminal emulator. 
- [Ghostty](https://github.com/ghostty-org/ghostty): a fast, feature-rich, and cross-platform terminal emulator that uses platform-native UI and GPU acceleration. 
- [Ptyxis](https://gitlab.gnome.org/chergert/ptyxis): A terminal for a container-oriented desktop
- [Wezterm](https://github.com/wez/wezterm): A GPU-accelerated cross-platform terminal emulator and multiplexer written by @wez and implemented in Rust 

### GUI

- [overskride](https://github.com/kaii-lb/overskride/issues): for bluetooth
- [zen](https://github.com/zen-browser/desktop)
- [zed](https://github.com/zed-industries/zed): Zed is a high-performance, multiplayer code editor from the creators of Atom and Tree-sitter

### Maybe

- [whisper-overlay](https://github.com/oddlama/whisper-overlay)
- [wkeys](https://github.com/ptazithos/wkeys)
- [cthulock](https://github.com/FriederHannenheim/cthulock)

### DE 

1. [Cosmic](https://github.com/pop-os/cosmic-epoch)
2. [Hyprland](https://github.com/hyprwm/Hyprland) WM combined with a suite of software to provide a DE

#### Hyprland

- [awww](https://codeberg.org/LGFae/awww) for wallpaper
- [quickshell](https://git.outfoxxed.me/quickshell/quickshell) for UI 
  - Inspirable UIs
    - [end-4](https://github.com/end-4/dots-hyprland)
    - [caelestia](https://github.com/caelestia-dots/shell)
  - Wanted features
    - Panel
    - Notifications
    - Maybe OSD
    - Log out
    - [Dev Toolbox](https://github.com/aleiepure/devtoolbox) features
- [wlr-which-key](https://github.com/MaxVerevkin/wlr-which-key) but get hyprland keybindings so no config is needed
- [clapboard](https://github.com/bjesus/clapboard)
- [swayosd](https://github.com/ErikReider/SwayOSD)
- [kooha](https://github.com/SeaDve/Kooha) for screen recording
- [wl-screenrec](https://github.com/russelltg/wl-screenrec):  High performance wlroots screen recording, featuring hardware encoding 
- [satty](https://github.com/Satty-org/Satty) for Modern Screenshot Annotation. 
- [shotman](https://git.sr.ht/~whynothugo/shotman) for screenshots
- [wleave](https://github.com/AMNatty/wleave?tab=readme-ov-file) logout prompt
- [anyrun](https://github.com/anyrun-org/anyrun) wayland runner
- [wayscriber](https://github.com/devmobasa/wayscriber): real-time screen annotation tool
- [vigiland](https://github.com/Jappie3/vigiland): idle behaviour inhibitor 
- Display Management
  - [kanshi](https://sr.ht/~emersion/kanshi/)
  - [shikane](https://gitlab.com/w0lff/shikane)
  - [cosmic rander](https://github.com/pop-os/cosmic-randr)
- [Pop Shell Keyboard Shortcuts](https://github.com/pop-os/shell-shortcuts)
- Plugins
  - [rustrland](https://github.com/mattdef/rustrland)
    - Expose
    - Shortcut Menu
    - Workspace Follow Focuse
    - System notifier
  - [Hypr Dynamic Cursor](https://github.com/VirtCode/hypr-dynamic-cursors) for shake to find mouse
  - hyprlock
  - hypridle
  - hyprsunset
  - [hyprland-monitor-attached](https://github.com/coffebar/hyprland-monitor-attached) run script when monitor is connected
  - [hyprnome](https://github.com/donovanglover/hyprnome) GNOME-like workspace switching
  - [hyprkool](https://github.com/thrombe/hyprkool) replicate the feel of kde activities and desktop grid layout
  - [hyprshell](https://github.com/H3rmt/hyprshell)
  - [hyprtasking](https://github.com/raybbian/hyprtasking)


## Potential For Fun & Hardwork

### Initramfs Generator

Create an intramfs generator starting from [microhop](https://github.com/tinythings/microhop) (use [3cpio](https://github.com/bdrung/3cpio) to operate on a manifest without needing to copy files into a temporary directory beforehand.) and port necessary sections of [booster](https://github.com/anatol/booster)

### Package Manager

Make a package manager that uses pkgar from [Redox OS's pkgutils](https://github.com/redox-os/pkgutils) and [AerynOS's moss](https://github.com/AerynOS/os-tools). Also maybe combine that with [AWS's tough](https://github.com/awslabs/tough?tab=readme-ov-file) to incorporate [The Update Framework](https://theupdateframework.io/).


## Notable Rust in Linux

- [PopOS](https://github.com/pop-os)
- [AerynOS](https://github.com/AerynOS)
- [CachyOS](https://github.com/cachyos)
