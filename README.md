# xuf - Xdevelnet universal format

Welcome! I'm looking for key-value format with arrays support, possible RAW binary data as value, easy editable in all text editors, without overbloated&fat library. And you know what? It's not exist. Until NOW! I decided to write it myself.

Goals:

1) Balance of simplicity and functionality

2) Possibility to edit with all text editors (if binary data present - with most text editors)

# Description with examples

#### Key names should be present as is, separated from value with newline (\n):
```
name
Bella
```
#### Key-value pairs should be separated with two newline characters (\n\n):
```
name
Bella

second name
Grace
```
#### If you need two newlines at value part - it should be escaped with slash character between newlines (\n\\\n):
```
Home address
Ukraine
Kyiv
\
01601, Bankova 2
```
#### Data can be united to arrays.
Format: open square bracket, newline, key names separated with newlines, close square bracket, array name. Array declaration should be placed right after all required key-value pairs.

*Warning: this arrays are not ASSOCIATIVE arrays. So, array in example below will NOT store key name, but only values; accessing person[2] will give you "Grace" string.*

```
name
Bella

second name
Grace

Home address
Ukraine
Kyiv
\
01601, Bankova 2

[
name
second name
Home address
] person
```
#### What if we don't want to think about key names - but need only array with data?
```
name
Bella

second name
Grace

Home address
Ukraine
Kyiv
\
01601, Bankova 2

[
name
second name
Home address
] person

applejack

rarity

pinkie pie

[3] ponies

```
#### Arrays with undefined elemets number:

```
one

two

three

four

five

six

seven

eight

nine

[] numbers
```
#### Data location can be also specified:
```
The

quick

brown

fox

jumps

over

above [] panagram part

dummy
key-value

below [] lazydog words

the

lazy

dog

```
You can omit above keyword if you want
```
what is love

baby don't hurt me

[] song lyric
```
#### Unreadable binary format:
1) RAW (read specified number of bytes right after \n)
```
raw below [106] weird_data

6y"��q6���oF�m�P�!�G�jPa���c�����!6=7!�M��
```
2) hexadecimal (may be in any case)
```
3679 22ef bfbd efbf bdef bfbd 7136 efbf bdef bfbd efbf bdef bfbd 6f46 efbf bdef bfbd 6def bfbd 50ef bfbd 21ef bfbd 47ef bfbd efbf bd6a efbf bd50 61ef bfbd efbf bdef bfbd efbf bd63 efbf bdef bfbd efbf bdef bfbd efbf bdef bfbd 2136 3d37 21ef bfbd 4def bfbd efbf bd

above hex [] weird_data
```
3) decimal (may be formatted if you want)
```
below decimal [] weird_data

  54 121  34 239 191 189 239 191 189 239 191 189 113  54 239 191
 189 239 191 189 239 191 189 239 191 189 111  70 239 191 189 239
 191 189 109 239 191 189  80 239 191 189  33 239 191 189  71 239
 191 189 239 191 189 106 239 191 189  80  97 239 191 189 239 191
 189 239 191 189 239 191 189  99 239 191 189 239 191 189 239 191
 189 239 191 189 239 191 189 239 191 189  33  54  61  55  33 239
 191 189  77 239 191 189 239 191 189
```
4) base64
```
below base64 [] weird_data

Nnki77+977+977+9cTbvv73vv73vv73vv71vRu+/ve+/vW3vv71Q77+9Ie+/vUfvv73vv71q77+9
UGHvv73vv73vv73vv71j77+977+977+977+977+977+9ITY9NyHvv71N77+977+9
```
5) escaped
```
something\0happens\there\n

escape [] test string
```
#### Specifying type is also possible with keywords
Type sizes:
  * octet - 8
  * short - 16
  * int - 32
  * long - 64
  * float - 32
  * double - 64

```
cash
65

card balance
1

int [
cash
card balance
] money

foot
27.1

breasts
96,2

float [
foot
breasts
] sizes
```

#### Private data
By default, multiple records with same key names should be ignored. But if you gonna collect them to array - you can clear "name space":
```
name
Andry

height
166

static [
name
height
] person1

name
Alla

height
170

static [
name
height
] person2

here is no "name" or "person" data aren't available

static []

free data cleanse

static []
```
#### Let's make a tree! And use indents!
```
hostname
example.com

port
8899

  static [
  hostname
  port
  ] host1

hostname
xdevelnet.org

port
1111

  static [
  hostname
  port
  ] host2

    static [
    host1
    host2
    ] hosts
```


#### Limitations
 * RAW array data will not (and should not) be escaped. After two newlines data wll be readed as many (in bytes) as defined.
 * Indents are not available for key-values.

#### Escaping

 * If you need square bracket at key name - it should be escaped with "\" symbol

#### Comparison

Compared to JSON, data can be present in both tree orders (from branches to partents and vice versa).

```
    static below [
    my blog
    my main website
    ] servers

  static below [
  host
  addr
  ] my blog

host
7.5.1.2

addr
someaddr.org

  static below [
  host
  addr
  ] my main website
  
host
35.245.245.9

addr
remoteaddr.com
```
