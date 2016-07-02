Introduction
============

Warning: This software is currently **alpha** and **untested**.  Don't use the
data blindly.

Kanji usage in Japan is regulated by the Jōyō Kanji table.  The latest, 2010
edition of the table is provided by the Ministry of Education in PDF format:
http://kokugo.bunka.go.jp/kokugo_nihongo/joho/kijun/naikaku/pdf/joyokanjihyo_20101130.pdf

The original table is quite messy and hard to use in computer programs.  This
project includes code to extract the data and convert it into popular formats:
TSV, JSON, SQL and HTML.  To minimize human error, the data is parsed
automatically as much as possible.  The results will be tested to ensure
consistency.

Most users won't have to run the scripts to extract the data; in the future,
you'll be able to download the output directly from this repository, in your
favourite format.


Roadmap/TODO
============
Completed:

 - On- and kun-readings
   - Romaji converter.
   - Distinguish special readings (marked in the table as indented/1字下げ).
 - Example words
   - Use examples to delimit okurigana in kun-readings
 - Old kanji
   - Handle 弁:[辨, 瓣, 辯].
   - Handle 亀/龜 as Unicode.
 - Variant forms
   - Encode accepted variants (許容字体) as Unicode variation sequences.
   - Handle problematic 叱 U+53F1 vs. 𠮟 U+20B9F situation (MEXT wants the
     latter, but everyone uses the former).
 - Notes (参考)
   - Save full note as text
     - Handle notes spanning multiple lines
 - Output formats
   - TSV
 - Tests
   - doctests for functions

Yet to be done:
 - Examples:
   - Handle POS markers like 〔副〕.
 - Notes (参考)
   - Distinguish kanji-scoped notes from reading-scoped (almost done; need to
     handle jukujikun better).
   - Parse and structure the data from notes
     - Alternative orthographies (同訓異字).
     - Pointers to reference section in text.
       - Extract example images.
     - Prefecture names.
     - Exceptional readings..
       - Unbounded lists (with a "などは").
         - Complement with all available examples from edict.
       - Alternatives ("とも").
     - Jukujikun/appendix readings.
       - Filter: only list them for kanji where the reading is not regular.
     - One-off types of notes.

 - Tests
   - old_kanji: against old dataset
   - readings: against Wikipedia table, kanjidic
   - examples: against edict
   - notes: write at least one test for each type of parsed data

 - Reference images for variant glyphs (許容字体)
 - Parse appendix

 - Output types:
   - SQL
   - JSON
   - HTML table

How to recreate the files
=========================

     pip3 install ostruct
     pip3 install regex # newer version of 're'
     git clone # this repo
     cd joyodb
     make # (needs Internet)
     bin/convert_joyodb

Output will be in `output/` directory.
