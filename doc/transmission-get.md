# transmission-get(1) -- download a given torrent

## SYNOPSIS
`transmission-get` [`-o`|`--output` .]  _torrent_<br>
`transmission-get` `-o`|`--output` _directory_ [`--`] _torrent_<br>
`transmission-get` `-h`|`--help`<br>

## DESCRIPTION
`transmission-get` downloads a given torrent file, torrent URI, or magnet URI.
It is a facade around `transmission-cli`, configuring `transmission-cli` to
exit immediately after finishing downloaing a torrent and to not create or
update any metadata files.

By default, `transmission-get` downloads into the working directory. The
`--output` option allows changing the download directory.

## OPTIONS
* -h, --help:
  Show help text and exit.
* -o, --output _directory_:
  Download to the specified directory.

## COPYRIGHT
`transmission-utils` (the package containing `transmission-get`) is
Copyright (c) 2016 Vinson Chuong under The MIT License.

## SEE ALSO
transmission-cli(1)
