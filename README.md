# Enigma cipher machine emulator

![](https://www.dropbox.com/s/5wb3u29ybxrzphl/Screenshot%202016-11-25%2015.34.47.png?dl=1)

This is a neat little emulator of various Enigma machines with a lot of
confugurable parameters. Somebody hurt your feelings by saying "my grandmother
encrypts better than you"? I've got you covered! With this port of the amazing
1940's technology you'll be just as good at encrypting things as anyone's
grandmother.

The CLI was modified by becgabri, I have added here the proper usage of the cli as well as the build procedure.

### Usage

This repository contains both the CLI tool and its underlying library written in Go.
The library is documented on [GoDoc](https://godoc.org/github.com/emedvedev/enigma).

As for the CLI tool, a simple `go get` could do it:

```
go get github.com/emedvedev/enigma/cmd/enigma
```
An alternative (I recommand) is to clone the github repository and compile the code on your machine:
in the directory ./enigma/cmd/enigma, you build the GO code by running:

```
go build .

```

The new CLI format developped by becgabri requires to put the arguments between  " " as the are manages as strings.
In the repository of the executable file you can run
```
./enigma -h
```
An example of the enigma configuration and out put is 

```
./enigma --rotors "Beta VI I III" --position "A A A A" --reflector "C" --plugboard "AD SF ET RY HK JL QZ WX UM OP" --rings "10 5 16 10" "hello world!"

```

which gives the following result:

```

Original text:
  hello world!

Processed original text:
  HELLOWORLDX

Enigma configuration:
  Rotors: Beta VI I III
  Rotor positions: A A A A
  Rings: 10 5 16 10
  Plugboard: AD SF ET RY HK JL QZ WX UM OP
  Reflector: C

Result:
  KZTDAUQBGVK
  
```

Much better! And of course, `enigma -h` will give you the complete description of
parameters and usage.

Importantly, since Enigma machines only have 26 keys, spaces are replaced with `X`,
and everything outside of the English alphabet is discarded. It's up to you to
come up with a suitable encoding.

Enjoy!

## Enigma models and features

Almost everything from the German Enigma machines can be configured in this
emulator:

* Rotor set: rotors from M3 and M4, the most famous Enigma machines, are
  pre-loaded.

* Reflector: reflectors A, B, C (as well as thin B and C versions for M4) are
  supported.

* Plugboard: any number of letter pairs is accepted. Plugboard configuration
  is optional.
Original text:
  hello world!

Processed original text:
  HELLOWORLDX

Enigma configuration:
  Rotors: Beta VI I III
  Rotor positions: A A A A
  Rings: 10 5 16 10
  Plugboard: AD SF ET RY HK JL QZ WX UM OP
  Reflector: C

Result:
  KZTDAUQBGVK
* Ring offsets and starting position of the rotors.

M3 and M4 can be fully emulated with the right parameters, and if it's
not enough, new rotors and reflectors can be added quite easily: just
add a new entry to the list in `rotors.go`, and that's it. Notches for
rotor turnover are optional.

Some exotic Enigma variants and implementations, as well
as devices such as Uhr, are not supported due to my chronic lack of
spare time. Your pull requests would be most welcome!

## Further reading

A bunch of material on Enigma machines, in no particular order. Explanations, specs,
other emulators.

- http://users.telenet.be/d.rijmenants/en/enigmatech.htm
- http://www.codesandciphers.org.uk/enigma/index.htm
- http://www.codesandciphers.org.uk/enigma/rotorspec.htm
- http://kerryb.github.io/enigma/
- http://enigma.louisedade.co.uk/enigma.html
- http://people.physik.hu-berlin.de/~palloks/js/enigma/enigma-u_v20_en.html
