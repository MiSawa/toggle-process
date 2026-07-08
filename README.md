# toggle-process

Toggle a process by repeatedly invoking the same command.

On the first invocation, `toggle-process` starts the command. While it is running, subsequent invocations send a signal to the process group instead of starting another instance.

## Installation

Install the `toggle-process` script somewhere in your `PATH`.

`toggle-process` requires `flock`, which is provided by `util-linux` on most Linux distributions.

## Usage

```text
Usage:
  toggle-process [OPTIONS] -- <COMMAND> [ARGS]...

Arguments:
  <COMMAND>  Command to run
  [ARGS]...  Arguments for the command

Options:
  --id <ID>           Instance ID (default: default)
  --state-dir <PATH>  State directory (default: ${TMPDIR:-/tmp}/toggle-process)
  -s SIGNAL           Signal to send (default: TERM)
  -h, --help          Show this help message
```

## Examples

Create a dropdown terminal:

```bash
toggle-process --id wezdrop -- \
    wezterm start --attach --domain wezdrop --class wezdrop-full
```

Then configure your window manager to make windows with class `wezdrop-full` fullscreen.

Run multiple independent toggles:

```bash
toggle-process --id music -- mpv ~/Music/radio.mp3
toggle-process --id notes -- obsidian
```

## Notes

* The command should remain in the foreground. Programs that daemonize or fork into the background are not supported.
* Signals are sent to the spawned process group, allowing child processes to terminate together with the main process.
* Runtime state is stored under `<state-dir>/<id>/`.

## Contribution

By contributing to this project, you agree that your contributions are licensed under the MIT License. Additionally, you grant the project maintainer a non-exclusive, perpetual, irrevocable, royalty-free, and sublicensable license to use, modify, and redistribute your contributions under any other license at the maintainer's discretion.
