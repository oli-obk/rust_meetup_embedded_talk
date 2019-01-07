# Embedded Rust

* stable?
* transcribing C
* Typed Hardware
* RTFM
* own your hardware

# Stability

2018 is over

Long live the 2018 edition

# rustup install

common ARM platforms are available on stable

```sh
rustup target add thumbv7em-none-eabihf
```

# build

choose target during build

```
cargo build --target thumbv7em-none-eabihf
```

# convenience build

choose target per crate

```toml
/// .cargo/config
[build]
target = "thumbv7em-none-eabihf"
```

# Transcribing C

Anything C can do Rust can do better

# Transcribing C

Anything C can do Rust can do ~~better~~

*But*: That's not why we write Rust

# Transcribing C

```C
int main() {
    *((int32_t*)0xF00BAA) = 42;
}
```

```Rust
fn main() {
    *(0xF00BAA as *const i32) = 42;
}
```

# Typed Hardware

```C
FOO_REGISTER |= SOME_FOO_FLAG;
```

```Rust
FOO_REGISTER |= SOME_FOO_FLAG;
FOO_REGISTER &= SOME_BAR_FLAG; // ERROR
```

# Ownership

Wait!

Stop!

# Ownership

```Rust
fn main(hardware: Hardware) {
    let Hardware {
        foo,
        bar,
        mut bump,
        ..
    } = hardware;
    foo.set_some_flag();
    let display_driver = Arc::new(Mutex::new(Display::new(bar, &mut bump)));
    let sound_driver = Sound::new(foo, &mut bump);
    let text_writer = Text::new(display_driver.clone());
    let plotter = Plotter::new(display_driver.clone());
    ...
}
```

# RTFM

**R**eal
**T**ime
**F**or the
**M**asses

# RTFM

* A framework
* Provable real time constraints
* Essentially the Ada tasking system
    * minus preemption
* magic
    * macro magic
    * lots of macro magic

# Overview

* Choose Your Weapon
* Reuse code via crates.io
* Share code with `wasm`
* not yet "trivially safe"
* not yet battle-proven in the world of certifications
