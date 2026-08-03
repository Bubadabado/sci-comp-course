---
---

# I/O Streams

Linux allows you to manipulate input and output streams (I/O streams). Input streams send data to a program. Output streams return data from a program. By default, your keyboard is the input stream on Linux, and your console is the output stream. There is also an error output stream which is dedicated to outputting errors from a program.

| Name | Purpose | File Descriptor | Default |
| --- | --- | --- | --- |
| `stdin` | Input | 0 | Keyboard |
| `stdout` | Normal output | 1 | Terminal |
| `stderr` | Error output | 2 | Terminal |

![A keyboard sends stdin to `bionano_software`, which has separate standard output (stdout, file descriptor 1) and standard error (stderr, file descriptor 2) streams.](../img/io-streams.png)

## Redirects

### `stdout`: "`>`" or "`>>`"

The greater-than token (`>`) redirects the standard output of a program to a new location. `grep` usually prints its results to the console. If you wanted to redirect it to a text file, you'd do the following:

```shell
# Create or replace output.txt
grep -i 'claws al ghul' catman_begins.txt > output.txt
# Create or append to output.txt
grep -i 'claws al ghul' catman_begins.txt >> output.txt
```

![A keyboard supplies stdin to the Linux `grep` command; its stdout stream is redirected to a text file while stderr remains directed toward the Linux terminal.](../img/io-redirect-stdout.png)

### `stderr`: "`2>`" or "`2>>`"

Prepending the output redirection tokens with a 2 redirects the standard error. Below is an example with the `vlc` media player.

```shell
# Create or replace error.log
vlc mr_smith_goes_to_pawshington.mpg 2> error.log
# Create or append to error.log
vlc mr_smith_goes_to_pawshington.mpg 2>> error.log
```

![A keyboard supplies stdin to the VLC media player; VLC's stdout is shown as a normal stream, while stderr is directed toward a warning output represented by a small portrait and warning symbol.](../img/io-redirect-stderr.png)

### Both `stdout` and `stderr`

You can combine the redirects to redirect both `stdout` and `stderr` at the same time:

```shell
bionano_software > output.log 2> error.log   # create
bionano_software >> output.log 2>> error.log # append
```

![A keyboard feeds stdin to `bionano_software`, whose stdout and stderr streams are shown leading to separate output destinations represented by a DNA symbol and a warning symbol.](../img/io-redirect-stdout-stderr.png)

### `stdin`: "`<`"

The less-than token is used to redirect standard input (`stdin`). It tells the program to take its input from the file following the token:

```shell
# Create a file or replace an existing file:
sort > sorted_cats.txt < cats.txt
# Another format example, albeit contrived:
sort < cats.txt > sorted_cats.txt
# Sort can take a filename as a direct argument without any input redirection, so the better syntax is:
sort cats.txt > sorted_cats.txt
```

![A diagram shows standard input feeding a Linux `sort` command, while the command produces standard output (stdout) and standard error (stderr) for the terminal.](../img/redirect-stdin.png)

### Combine streams

One I/O stream can be redirected to another I/O stream. This is the syntax for redirecting `stderr` to `stdout`. It would ensure that all output, standard or error, would end up at the destination:

```shell
ping -c 10 procatinator.com > output.txt 2>&1
ping -c 10 procatinator.com &> output.txt # shorthand
```

### Discard output

`/dev/null` can be thought of as a black hole. It's a special device that discards anything that is passed to it. The ampersand-greater-than (`&>`) will redirect both streams to the same place:

```shell
./automated_task.sh &> /dev/null # run the program, throwing away all output
```

![A keyboard sends stdin to `automated_task.sh`, which redirects stdout and stderr to a blackhole indicating that the command’s output streams are discarded.](../img/io-discard-output.png)
