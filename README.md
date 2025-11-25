# rtgz

Recursively find, compress, and optionally delete subfolders or files matching a pattern.

## Installing

Copy rtgz to your path (e.g., ~/bin) and make it executable:
```shell
mkdir -p ~/bin
cp rtgz ~/bin
chmod +x ~/bin/rtgz
```

## Usage

```shell
rtgz "<pattern>" [start_dir] [options]
```

Remember to quote wildcards with regular expressions, e.g. "*.log", etc.

## Options

| Flag | Description |  
| ---- | ----------- |  
| -f, --file    | File Mode: Search for files instead of folders. Groups matches by directory. |  
| -d, --delete  | Delete Mode: Delete original items after successful compression. |  
| -t, --test    | Test Mode: Dry-run. Lists found items but takes no action. |  
| -v, --version | Print version and exit. |  
| -h, --help    | Show help message. |  

## Examples

### Folder Mode (Default)

Finds matching folders and compresses them individually. The command:
```shell
rtgz "*success" experiments
```

results in:
```dir
experiments/
├── exp_01_failed/
├── exp_01_success/        <- Kept (unless -d is used)
├── exp_01_success.tar.gz  <- Created
...
```

### File Mode (-f)

Finds matching files, groups them by directory, and creates one archive per folder.
```shell
rtgz "*.log" project -f
```

The archive name is derived from the pattern, wildcards removed.

```dir
project/
├── backend/
│   ├── log.tar.gz   <- Contains error.log & access.log
│   ├── error.log
│   └── access.log
...
```

### Delete Mode (-d)

Deletes original files or folders, only if the compression succeeds.

```shell
rtgz "data_*" -f -d
```

### Test Mode (-t)

Previews operations without modifying data.
```shell
rtgz "*.old" -f -t
```

It lists the matches:
```shell
Target:       '*.old'
Path:         '/home/user/docs'
Compressing:  files (as old.tar.gz)
Action:       testing

Found 15 files in: /home/user/docs/2022
Found 76 files in: /home/user/docs/2023
```

## Contributing

Do you want to contribute? Feel free to open an issue or a pull request!  :D
