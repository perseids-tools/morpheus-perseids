# Morpheus Perseids

Morpheus is a morphological parsing tool originally written as part of the Perseus Project.
It takes Ancient Greek or Latin text as input and performs a morphological analysis.

Morpheus Perseids is a fork of the Alpheios Project version of
[Morpheus](https://github.com/alpheios-project/morpheus)
which is used by the
[morph.perseids.org](http://morph.perseids.org/analysis/word?lang=grc&engine=morpheusgrc&word=%E1%BC%84%CE%BD%CE%B8%CF%81%CF%89%CF%80%CE%BF%CF%82)
API.

## Building

### Docker

#### From Docker Hub

```bash
docker pull perseidsproject/morpheus-perseids

docker run -it perseidsproject/morpheus-perseids /bin/bash
```

(See project on [Docker Hub](https://hub.docker.com/r/perseidsproject/morpheus-perseids/).)

#### Building container

```
docker build -t morpheus-perseids .

docker run -it morpheus-perseids /bin/bash
```

### macOS

Requirements:

- Xcode command line tools

```bash
cd src/
make clean
CFLAGS='-std=gnu89 -Wno-return-type' make LOADLIBES='-ll'
make install
```

(Tested on macOS High Sierra Version 10.13.5, Apple LLVM version 9.1.0.)

### Linux

Requirements:

- `make`
- `gcc`
- `flex`

```bash
cd src/
make clean
CFLAGS='-std=gnu89' make
make install
```

(Tested on Ubuntu 16.04 and 18.04.)

## Usage

Example usage:

```
$ MORPHLIB=stemlib bin/morpheus 'a)/nqrwpos'
<words>
<word>
<form xml:lang="grc-x-beta">a)/nqrwpos</form>
<entry>
<dict>
<hdwd xml:lang="grc-x-beta">a)/nqrwpos</hdwd>
<pofs order="3">noun</pofs>
<decl>2nd</decl>
<gend>masculine</gend>
</dict>
<infl>
<term xml:lang="grc-x-beta"><stem>a)nqrwp</stem><suff>os</suff></term>
<pofs order="3">noun</pofs>
<decl>2nd</decl>
<case order="7">nominative</case>
<gend>masculine</gend>
<num>singular</num>
<stemtype>os_ou</stemtype>
</infl>
</entry>
</word>
</words>
```

```
$ MORPHLIB=stemlib bin/morpheus -L 'cactus'
<words>
<word>
<form xml:lang="lat">cactus</form>
<entry>
<dict>
<hdwd xml:lang="lat">cactus</hdwd>
<pofs order="3">noun</pofs>
<decl>2nd</decl>
<gend>masculine</gend>
</dict>
<infl>
<term xml:lang="lat"><stem>cact</stem><suff>us</suff></term>
<pofs order="3">noun</pofs>
<decl>2nd</decl>
<case order="7">nominative</case>
<gend>masculine</gend>
<num>singular</num>
<stemtype>us_i</stemtype>
</infl>
</entry>
</word>
</words>
```

### Command line options

| Option | Description |
| - | - |
| -L | Set language to Latin |
| -i | Show more detailed output |
| -V | Analyze verbs only. |
| -S | Turn off Strict case. For Greek, this allows words with an initial capital to be recognized. For languages in the Roman alphabet, allows words with initial capital or in all capitals. |

## Tests

Requirements:

- `ruby` (~3.0)

`./test/test.rb`

