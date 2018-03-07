# Convert EPWING dictionaries to a kindle-readable format (Japanese)

<p align="center">
<img src="images/demo.jpeg" alt="Result demonstration" width="450" />
<br/>
<sup>Demonstration of the final result</sup>
</p>

# Table of Contents

  * [Todo](#todo)
  * [Process description](#process-description)
  * [Usage](#usage)
     * [Requirements](#requirements)
     * [EPWING to JSON (yomichan)](#epwing-to-json-yomichan)
     * [JSON to Tab (yomi2tab)](#json-to-tab-yomi2tab)
     * [Tab to OPF (tab2opf)](#tab-to-opf-tab2opf)
  * [OPF to mobi (kindlegen)](#opf-to-mobi-kindlegen)
  * [Miscellaneous](#miscellaneous)
     * [Another way to convert epwing](#another-way-to-convert-epwing)
     * [Why would you ever do this? Kindle offers free builtin dictionaries!](#why-would-you-ever-do-this-kindle-offers-free-builtin-dictionaries)
     * [Shoutouts](#shoutouts)

## Todo

- [x] Convert EPWING dictionary to kindle
- [x] Proper formatting, newlines are rendering as they should be
- [x] \(mostly) Optional "Simple" mode without old ways to write a word that use outdated kana 
- [x] Support kanji when the entry is formatted as `[Kanji/Hiragana]Katakana[K/H]`
- [x] Multiple entries for the same word (not merging all of the definitions into one; official kindle dictionaries function in this way)
- [x] Tested with 大辞林
- [ ] Add a zsh/python script for processing everyhting automatically
- [ ] Better sorting for multiple entries
- [ ] Test more dictionaries 
- [ ] Improve performance (low priority)
- [ ] Make it possible to look up suffixes (stuff like -好き; low priority)
- [ ] Make it possible to look up phrases with `=` in their key (It's probably another weird EPWING thing; low priority)

*Note*: this process was tested using スーパー大辞林, using it with other dictionaries like 新明解国語辞典 should still work but some unexpected problems may arise. If you manage to successfully import another dictionary using this repo, please add a photo of your final result to the images folder via a pull request.

## Process description

![Process flowchart](images/flowchart.svg)

In order to convert an EPWING dictionary to kindle, you first have to follow the process displayed above: first you convert the EPWING to a stardict format (TAB-separated), then using tab2opf you can convert it to opf (html) dictionary and then generate a mobi file using kindlegen.

## Usage

### Requirements: 

- [python 3.6 or higher](https://www.python.org/)
- [yomichan-import](https://foosoft.net/projects/yomichan-import/)
- [kindlegen](https://www.amazon.com/gp/feature.html?docId=1000765211)
- `pip3 install -r requirements.txt` for python requirements

### EPWING to JSON (yomichan)

```
./yomichan-import
```

### JSON to Tab (yomi2tab)

```
pip3 install -r requirements.txt
python3 yomi2tab.py -o dict.tab data
```

Yomichan-import generates an archive file, that you have to unzip into a folder (called `data` in the above example) for `yomi2tab` to work.

### Tab to OPF (tab2opf)

This repository provides a japanese-specific tab2opf tool with some improvements (adding progress indicators, correct display of `<`/`>`, etc.). It is based on https://github.com/apeyser/tab2opf by Alexander Peyser from 2015 which itself is based on the generally available tab2opf.py by Klokan Petr Přidal (www.klokan.cz) from 2007.

```
python3 tab2opf.py dict.tab
```

## OPF to mobi (kindlegen)

```
kindlegen opf/dict.opf
```

In order to generate a .mobi dictionary from OPF, you can use a tool called `kindlegen` that's provided by amazon. It may take a while but doesn't require any extra work.

After you've generated a .mobi dictionary, you can import it into [calibre](https://calibre-ebook.com) to edit the metadata, add a cover picture and send it to kindle.

## Miscellaneous

### Another way to convert epwing

We can also use the noj format as an intermediary between the EPWING dictionary and the tab file. 

**Steps:**

1. https://github.com/mcho421/noj_dumpers
	*  Don't bother with compiling it because won't work, just copy your files to the noj_dumper folder and then `python2 noj_dumper.py epwing_folder`
2. https://github.com/asika/noj2tab (you can try reading the Chinese blog post with google translate)
3. Tab2Opf (mine or https://github.com/apeyser/tab2opf)
4. kindlegen + calibre

### Why would you ever do this? Kindle offers free builtin dictionaries!

デジタル大辞泉　provided with Kindle doesn't have pitch accent marks.

### Shoutouts

[Cophnia61](https://forum.koohii.com/user-4654.html) - https://forum.koohii.com/thread-14949.html

[gh-md-toc](https://github.com/ekalinin/github-markdown-toc) - *the* TOC generator for github
