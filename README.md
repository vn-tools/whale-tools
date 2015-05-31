whale-tools
---

This repository contains fan translation tools for Whale-based games.

Currently it supports only Tsujidou-san no Junai Road, but it shouldn't be too
difficult to add support for other games - it should boil down to changing
constants inside `archiver` and using different `filenames.lst` file.

Basic workflow:

- Run `archiver` to extract `*.dat` archives.
- Edit the files.
- Run `archiver` again to pack folders back into `*.dat` archives.

### General repacking

- You need Python 3, preferably 3.4.3.
- To see list of options, run `./archiver --help`.
- The game executables are most likely protected with Themida protector,
  meaning it's difficult to tamper with its binary code for stuff such as
  repositioning text etc. Fortunately it's not needed, since 99% of game logic
  resides in 100%-reversible script files.

### Scripts

- The scripts are encoded with Shift-JIS of course.
- The scripts are implemented in a way that anything that starts with
  ASCII characters is treated as code. I haven't looked too much if you can
  render a text through some script routines, but I successfully changed the
  text when I prepended the text with a full-width space.
- This script doesn't include word wrapping. I can't think of any productive
  way to solve this problem so I leave it to people with more experience. Pull
  requests are encouraged.

### Images

- The archives don't provide file names and use CRC checksums of the names (NOT
  checksums of contents) instead. The file names are absolutely needed to
  extract anything but scripts. Therefore, you need to pass
  `--filenames=list_of_file_names.lst` to `archiver`. I included an example
  file list for Tsujidou-san no Junai Road (a bit more exhaustive than
  asmodean's list), but it's still not complete. This means you almost surely
  *will* get "file not found" errors at some point. These can be fixed by
  adding the file name the game complains about to file names list and
  repacking the archives. Consider firing a pull request if you find such
  files. (There is also `hash_finder` that is supposed to aid brute-force based
  hash discovery.)
- The images are based on TLG file format.
      - To convert PNG back to TLG, you can use tools bundled with Kirikiri
        game engine (`krkrtpc.exe` that can be downloaded
        [here](http://tlwiki.org/images/6/6d/KiriKiri_Official_Tools_English_Translation.zip),
        if the link is down, see TLWiki).
      - To convert TLG to PNG, you can use the tool above or
        [arc_unpacker](https://github.com/vn-tools/arc_unpacker). `krkrtpc`
        failed to convert some of TLG files to PNG while `arc_unpacker` managed
        to do so.

### Proof it works

![2015-05-31-115911_1920x1078_escrotum](https://cloud.githubusercontent.com/assets/1045476/7901526/9a8b8106-078c-11e5-84da-1de0848d858f.png)

### References

- http://asmodean.reverse.net/pages/exwhaledat.html
- Carter Yagemann's scripts
