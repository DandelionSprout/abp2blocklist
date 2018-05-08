# abp2blocklist

This is a script to convert [Adblock Plus filter lists](https://adblockplus.org/filters)
to [WebKit block lists](https://www.webkit.org/blog/3476/content-blockers-first-look/).

Note that WebKit content blockers are fairly limited. Hence, not all filters
can be converted (in a compatible way), and some differences compared to Adblock
Plus for other browsers are expected.

This script is used to convert the filter lists for
[Adblock Plus for iOS](https://adblockplus.org/releases/adblock-plus-10-for-ios-released).

## Requirements

The required packages can be installed via [NPM](https://npmjs.org):

```
npm install
```

### filterClasses.js

The filterClasses module in `node_modules/filterClasses.js` is generated from
the module in the `adblockpluscore` repository. It has been generated using
JS Hydra, and small modifications made. If you need to re-generate the file run
this command (adjusting the paths as appropriate):

```
python buildtools/jshydra/abp_rewrite.py adblockpluscore/lib/filterClasses.js | grep -vi filterNotifier > ../abp2blocklist/node_modules/filterClasses.js
```
You will then need to remove any references to the `utils` module from the
generated file by hand.


## Usage

We recommend the use of [Node.js](https://nodejs.org/en/download/)'s own command prompt, but it should also work in regular Unix command prompts (e.g. Cygwin). In either case the command is:
```
node abp2blocklist.js < easylist.txt > easylist.json
```

We don't recommend using PowerShell, since it adds bloated metadata that increases the size of the output file, but if so needed, the following command can be used there:
```
get-content easylist.txt | node abp2blocklist.js > easylist.json
```

Both possibilities assume that you're trying to convert an input file that'd be called _easylist.txt_, and that you've navigated to the file's correct folder through the _cd_ command. If the input file has a different name, replace _easylist.txt_ with the file's name.

## Tests

Unit tests live in the `tests/` directory. To run the unit tests ensure you have
already installed the required packages (see above) and then type this command:

```
npm test
```
