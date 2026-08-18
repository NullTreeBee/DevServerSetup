# DevServerSetup

Turn a Mac into a temporary Ollama development server that can be reached from a phone through Open WebUI Computer and Tailscale.

The single `server-mode` command:

- installs missing dependencies;
- starts Ollama and Open WebUI Computer;
- enables private phone access through Tailscale;
- prevents system sleep while the Mac is plugged in, while allowing the display to turn off;
- reverses those changes when server mode is switched off.

## Install

Clone the repository and run:

```bash
zsh ./server-mode install
```

The installer checks for and, where necessary, installs:

- Homebrew
- `uv`
- Open WebUI Computer (`cptr`)
- Ollama
- Tailscale

Tailscale may require approval in macOS System Settings and an interactive sign-in. The script cannot perform that account sign-in for you.

Open a new Terminal after installation.

## Use

```bash
server-mode on
server-mode status
server-mode off
```

You can also run it directly without installing the command:

```bash
zsh ./server-mode on
```

`server-mode on` is safe to run again if the services are already running. Anything that was already running before the script started is left running by `server-mode off`.

Computer listens locally on `127.0.0.1:8000`. After startup, Tailscale prints the HTTPS address to open from your phone. Both devices must be signed into the same Tailscale account.

On the first Computer launch, complete its one-time account setup on the Mac. Then connect Ollama from Computer using:

```text
Provider: OpenAI
Base URL: http://localhost:11434/v1
API key: ollama
```

Ollama models are deliberately not downloaded automatically because they can be large. Install the model you want separately, for example:

```bash
ollama pull <model-name>
```

Logs and PID files are stored in:

```text
~/.local/state/server-mode
```

Set `CPTR_PORT` before running the command if port `8000` is already in use.
