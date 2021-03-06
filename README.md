goupx - Fix golang Linux ELF executables to work with upx
---------------------------------------------------

## Update: 2016/03/10

As far as I (pwaller) know, goupx is no longer necessary for Linux binaries since it was fixed in
go1.6.

## About

Installation: `go get github.com/pwaller/goupx`

(or if you don't want to do it with root, `GOPATH=${HOME}/.local go get github.com/pwaller/goupx` will install it to `${HOME}/.local/bin/goupx`).

Usage: `goupx [filename]`

Fixes the `PT_LOAD` offset of [filename] and then runs `upx`.

This is only necessary for Linux ELF executables (not Mach-O executables or windows binaries, for example).

Based on [code found on the upx bugtracker](http://sourceforge.net/tracker/?func=detail&atid=102331&aid=3408066&group_id=2331).

MIT licensed.

Fixes the following issue
=========================

    $ upx [linux ELF go binary]
                           Ultimate Packer for eXecutables
                              Copyright (C) 1996 - 2011
    UPX 3.08        Markus Oberhumer, Laszlo Molnar & John Reiser   Dec 12th 2011

            File size         Ratio      Format      Name
       --------------------   ------   -----------   -----------
    upx: goupx: EOFException: premature end of file                                

    Packed 1 file: 0 ok, 1 error.

Typical compression ratio
=========================

Resulting filesizes are typically 25% of the original go executable. Your mileage my vary.
