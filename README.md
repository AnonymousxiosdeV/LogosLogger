## Logos logging script

This (specifically, `log.py`) is a script that I've been using to parse an objective-c header file and return output that can be piped into a logos file to log every single time that the functions in that header file is called.

### To run:

```
./log.py <options> /path/to/header/file.h
```

### Options:
`-h`, `--help`: Shows help message \
`-n`, `--newline`: Removes all newlines from the string that is being logged so that it doesn't appear on multiple lines and you can more easilier filter with programs like grep. \
`-f`, `--file`: Outputs result of logs to a file instead of to `NSLog`, since `NSLog` truncates output at a certain point \
`-s`, `--sep` : Parses the file as a list of functions from different files. If you use this option, all lines in the file you're telling it to parse should look something like this: `./relative/path/to/file.h:23:-(void)function;`. To get a file with these lines, I normally just run `grep` through all the headers. For example, if I wanted all functions that had the string `conversation`, I would run `grep -rni "conversation" > parse.txt` and then `log.py -s ./parse.txt` to get the logos log file.

You can pipe the standard output from this script directly into a `.x` logos file, then build & install it and watch the output of the console/oslog (or view the file, if you called the `-f`/`--file` flag) for every time each of those functions is called.

Feel free to open an issue or contribute if something's not right or you'd like a feature added.