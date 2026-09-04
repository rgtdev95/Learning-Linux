# The `touch` Command

`touch` is primarily used to update a file's access and modification timestamps to the current system time. It also serves a second purpose: if the specified file does not exist, `touch` creates it as an empty file — a common way to generate placeholders for future use.

## Setting a Specific Timestamp

The `-t` option sets the access and modification timestamps to a specific value, using the format `[[CC]YY]MMDDhhmm[.ss]`. To set a file's timestamp to 4:00 p.m. on December 9th:

```bash
$ touch -t 12091600 myfile
```

Here, `12` is the month, `09` is the day, `16` is the hour, and `00` is the minute (the year defaults to the current year since it wasn't specified).

> [!NOTE]
> The file's **change time** (`ctime`) works differently — it isn't something `touch` lets you set directly. Instead, `ctime` is automatically updated to the real current time whenever a file's metadata changes, and running `touch -t` to alter `atime`/`mtime` counts as such a change. So after this command, `ctime` reflects the moment `touch` was run, not December 9th.
