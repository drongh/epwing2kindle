# Convert EPWING dictionaries to a kindle-readable format (Japanese)

<img src="demo.jpeg" alt="Result demonstration" style="width: 300px; display: block;"/>
*Demonstration of the final result*

## Process description


## Usage

### EPWING to JSON (yomichan)

```
./yomichan-import
```

### JSON to Tab (yomi2tab)

```
python3 yomi2tab.py -fl data -o test_p.tab
```

### Tab to OPF (tab2opf)

This repository provides a japanese-specific tab2opf tool with some improvements (adding progress indicators, correct display of `<`/`>`, etc.). It is based on https://github.com/apeyser/tab2opf by Alexander Peyser from 2015 which itself is based on the generally available tab2opf.py by Klokan Petr Přidal (www.klokan.cz) from 2007.

```
python3 tab2opf.py -s jp -t jp test_p.tab
```

## OPF to mobi (kindlegen)

```
kindlegen -verbose test_p.opf
```

Then you can import your .mobi file into [calibre](https://calibre-ebook.com) to edit the metadata, add the cover picture and send it to kindle.

## Miscallaneous

### Other way to convert epwing

We can also use the noj format as an intermediary between the EPWING dictionary and the tab file. 

**Steps:**

1. https://github.com/mcho421/noj_dumpers
	
	*  Don't bother with compiling it because won't work, just copy your files to the noj_dumper folder and then `python2 noj_dumper.py epwing_folder`
2. https://github.com/asika/noj2tab
3. Tab2Opf (mine or https://github.com/apeyser/tab2opf)
4. kindlegen + calibre

### Why would you ever do this? Kindle offers free builtin dictionaries!

デジタル大辞泉　provided with Kindle doesn't have pitch accent marks.

### IS THE PICTURE A ゴゴゴ REFERENCE????

Yes ;)