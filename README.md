# xuf
Xdevelnet universal format

Welcome! I'm looking for key-value format with arrays support, possible RAW binary data as value, easy editable in all text editors, without overbloated&fat library. And you know what? It's not exist.

I decided to write it myself.

Goals:
1) Balance of simplicity and functionality
2) Possibility to edit with all text editors (if binary data present - with most text editors)

# Descriptions with examples

#### Key names should be present as is, separated from value with newline (\n).
```
name
Bella
```
#### Key-value pairs should be separated with two newline characters (\n\n).
```
name
Bella

second name
Grace
```
#### If you need two newlines at value part - it should be escaped with slash character between newlines (\n\\n)
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

So, as you can see, this array just "collect" key-free data. If there is more key-free data present (like this string), then arrays collected - it will be collected later to special array OR ignored (depending on import config). Feel free to use it as comments.
```
#### Arrays with undefined elemets number. Just put keyword "collect" before array declaration.
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

collect [
] numbers
```
#### Unreadable binary data will (should) be escaped, but you may wish to store it as is for some cases.
Declare array, which points to data right AFTER array declaration and elements numbers should represend number of RAW bytes stored. Use "below" keyword for that purpose.
```
below [91] weird_data

6y"��q6���oF�m�P�!�G�jPa���c�����!6=7!�M��
```
#### Limitations

 * There is no data types. Like I said, format should be simple. If your application expecting integer - you should convert it from string. Belive me or not, it's good.
 * There is no possibility to make arrays with arrays (array with reference to array). Maybe, it will be added later.
 * RAW array data will not (and should not) be escaped. After two newlines data should be readed as many as defined.
