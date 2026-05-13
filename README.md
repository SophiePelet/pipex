# pipex

A 42 project that reproduces shell piping behavior using low-level Unix system calls (`fork`, `pipe`, `dup2`, `execve`, `waitpid`).

## Build

```bash
make
```

Build bonus version (multi-command pipeline + `here_doc`):

```bash
make bonus
```

Clean files:

```bash
make clean
make fclean
make re
```

## Mandatory usage

```bash
./pipex infile "cmd1" "cmd2" outfile
```

Equivalent shell behavior:

```bash
< infile cmd1 | cmd2 > outfile
```

Example:

```bash
./pipex input.txt "grep hello" "wc -l" output.txt
```

## Bonus usage

Multiple commands:

```bash
./pipex infile "cmd1" "cmd2" ... "cmdN" outfile
```

`here_doc` mode (appends to outfile):

```bash
./pipex here_doc LIMITER "cmd1" "cmd2" ... "cmdN" outfile
```

Equivalent shell behavior:

```bash
cmd1 << LIMITER | cmd2 | ... | cmdN >> outfile
```

## Notes

- Commands are resolved through `PATH` (or used as absolute/relative paths when provided).
- Command strings are split on spaces, so advanced shell quoting is not fully handled.
- On command-not-found or execution failures, error messages are printed to stderr.

## Grade

125/100
