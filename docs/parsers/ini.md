
# jc.parsers.ini
jc - JSON CLI output utility `INI` file parser

Parses standard `INI` files and files containing simple key/value pairs. Delimiter can be `=` or `:`. Missing values are supported. Comment prefix can be `#` or `;`. Comments must be on their own line.

Note: Values starting and ending with quotation marks will have the marks removed. If you would like to keep the quotation marks, use the `-r` command-line argument or the `raw=True` argument in `parse()`.

Usage (cli):

    $ cat foo.ini | jc --ini

Usage (module):

    import jc.parsers.ini
    result = jc.parsers.ini.parse(ini_file_output)

Compatibility:

    'linux', 'darwin', 'cygwin', 'win32', 'aix', 'freebsd'

Examples:

    $ cat example.ini
    [DEFAULT]
    ServerAliveInterval = 45
    Compression = yes
    CompressionLevel = 9
    ForwardX11 = yes

    [bitbucket.org]
    User = hg

    [topsecret.server.com]
    Port = 50022
    ForwardX11 = no

    $ cat example.ini | jc --ini -p
    {
      "bitbucket.org": {
        "serveraliveinterval": "45",
        "compression": "yes",
        "compressionlevel": "9",
        "forwardx11": "yes",
        "user": "hg"
      },
      "topsecret.server.com": {
        "serveraliveinterval": "45",
        "compression": "yes",
        "compressionlevel": "9",
        "forwardx11": "no",
        "port": "50022"
      }
    }


## info
```python
info()
```


## process
```python
process(proc_data)
```

Final processing to conform to the schema.

Parameters:

    proc_data:   (Dictionary) raw structured data to process

Returns:

    Dictionary representing an ini or simple key/value pair document:

    {
      ini or key/value document converted to a dictionary - see configparser standard
      library documentation for more details.

      Note: Values starting and ending with quotation marks will have the marks removed.
            If you would like to keep the quotation marks, use the -r or raw=True argument.
    }


## parse
```python
parse(data, raw=False, quiet=False)
```

Main text parsing function

Parameters:

    data:        (string)  text data to parse
    raw:         (boolean) output preprocessed JSON if True
    quiet:       (boolean) suppress warning messages if True

Returns:

    Dictionary representing the ini file

