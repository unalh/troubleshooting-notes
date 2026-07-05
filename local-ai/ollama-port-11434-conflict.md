# Ollama Port 11434 Conflict

## Problem

Ollama failed to start because port 11434 was already in use.

## Symptoms

- Ollama service could not start.
- Connection to `localhost:11434` failed.
- Another process appeared to be using the port.

## Investigation

Checked which process was listening on port 11434:

```powershell
netstat -ano | findstr :11434
```

Then identified the process by its PID:

```powershell
tasklist | findstr <PID>
```

## Solution

Stopped the conflicting process and restarted Ollama:

```powershell
taskkill /PID <PID> /F
```

## Result

Ollama successfully started and responded on `localhost:11434`.

## What I Learned

Always verify port ownership before reinstalling or reconfiguring a local service.
