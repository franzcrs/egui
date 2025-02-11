# egui

Egui crates using tao with modified dependencies, for solving gtk-sys/gtk version conflicts.

Cargo Build Error:
```
    Updating crates.io index
    Updating git repository `https://github.com/franzcrs/tauri-egui.git`
error: failed to select a version for `gtk-sys`.
    ... required by package `gtk v0.16.0`
    ... which satisfies dependency `gtk = "^0.16"` of package `tao v0.18.0`
    ... which satisfies dependency `winit = "^0.18.0"` of package `eframe_tao v0.23.0`
    ... which satisfies dependency `eframe = "^0.23.0"` of package `tauri-egui v0.3.0 (https://github.com/franzcrs/tauri-egui.git?branch=dev-franzcrs#78688412)`
    ... which satisfies git dependency `tauri-egui` of package `app v0.1.0 (/app_path)`
versions that meet the requirements `^0.16` are: 0.16.0

the package `gtk-sys` links to the native library `gtk-3`, but it conflicts with a previous package which links to `gtk-3` as well:
package `gtk-sys v0.18.0`
    ... which satisfies dependency `ffi = "^0.18"` of package `gtk v0.18.0`
    ... which satisfies dependency `gtk = "^0.18"` of package `tao v0.23.0`
    ... which satisfies dependency `tao = "^0.23"` of package `app v0.1.0 (/app_path)`
Only one package in the dependency graph may specify the same links value. This helps ensure that only one copy of a native library is linked in the final binary. Try to adjust your dependencies so that only one package uses the `links = "gtk-3"` value. For more information, see https://doc.rust-lang.org/cargo/reference/resolver.html#links.

failed to select a version for `gtk-sys` which could resolve this conflict
```

> egui (pronounced "e-gooey") is a simple, fast, and highly portable immediate mode GUI library for Rust.
>
> egui aims to be the easiest-to-use Rust GUI library, and the simplest way to make a web app in Rust.

[![](https://img.shields.io/crates/v/egui.svg)](https://crates.io/crates/egui)
[![Docs.rs](https://docs.rs/egui/badge.svg)](https://docs.rs/egui)

```
[dependencies]
egui = "0.22.0"
```

This repository provides binding for egui to use tao instead. Currently only `glow` backend is supported.

For more information on how to use egui, please check out [egui repository](https://github.com/emilk/egui) for both [simple examples](https://github.com/emilk/egui/tree/master/examples) and [detailed documents](https://docs.rs/egui).

## Who is egui for?

Quoting from egui repository:

> [...] if you are writing something interactive in Rust that needs a simple GUI, egui may be for you.

## Demo

Demo app uses [`eframe_tao`](https://github.com/tauri-apps/egui/tree/master/crates/eframe).

To test the demo app locally, run `cargo run --release -p egui_demo_app`.

The native backend is [`egui_glow_tao`](https://github.com/tauri-apps/egui/tree/master/crates/egui_glow) (using [`glow`](https://crates.io/crates/glow)) and should work out-of-the-box on Mac and Windows, but on Linux you need to first run:

`sudo apt-get install -y libclang-dev libgtk-3-dev libxcb-render0-dev libxcb-shape0-dev libxcb-xfixes0-dev libxkbcommon-dev libssl-dev`

On Fedora Rawhide you need to run:

`dnf install clang clang-devel clang-tools-extra libxkbcommon-devel pkg-config openssl-devel libxcb-devel gtk3-devel atk fontconfig-devel`

**NOTE**: This is just for the demo app - egui itself is completely platform agnostic!
