- 👋 Hi, I’m @MasterLocal
- 👀 I’m interested in Localization solutions, OKRs, KPIs, metrics and content tests to scale products
- 🌱 I’m currently learning Chinese, Hebrew and Arabic, while I am fluent in 7 and familiar with 30 languages.
- 💞️ I’m looking to collaborate on NLP processes, using spacy for new markets
- 📫 How to reach me michele.santamaria@gmail.com

The purpose of this file is to share basic requirements for spacy 3.0 and L10n applications including python scripts for AI and internationalization.

Localization-Base

This is the common root of all Localization projects. Each project gets its own long-term branch, based on this root.
Layout

We follow the Maven Standard Directory Layout, to make it easy to write string processors in JVM-based languages, and publish resource packages in various formats to Nexus. This can coexist with alternative packaging systems like BuildTools, which publishes to tar1.
Commit source string documents to the following location. This is also known as the path filter in SmartlingLink:
src/main/resources/strings/source
Localized string documents will automatically be committed from the translation provider into the following location. This is also known as the commit path in SmartlingLink:
src/main/resources/strings/derived
Merge Policy

Only changes to the common base that affect all projects should be branched from, and merged to, master. This would include things like bugfixes or feature additions to the common packaging infrastructure.
Changes for a specific project should be branched from, and merged to, a long-term branch named after the project.
Project branches should never be merged to master.
Project Branches

After creating a new project branch, remember to change the artifactId in pom.xml.
UXStrings

convert.py is a Python script that rewrites Microsoft Excel spreadsheets from UX Master Strings format into strings.json format.
convert.py runs on Python version 2.7 and >= 3.5. It has been tested on Windows 10, and should work on Windows, MacOS X, and Linux. Failure to run on any of these platforms is a bug; please report it to caseyc@telenav.com.
Usage

On Windows, you can drag an Excel spreadsheet onto the convert.py icon, and it will create strings-{locale}.json files for all of the locales present in the spreadsheet.
On MacOS X, you can do the same thing with Macintosh_convert.app.
On Linux, or if you prefer the command line, here is the usage description:
$ python convert.py --help

usage: Convert UX Strings documents into whatever format LocaleLink needs.
       [-h] [--from FROM_FMT] [--to TO_FMT] [--locale LOCALE] [--out OUT_DIR]
       filenames [filenames ...]

positional arguments:
  filenames             The files to process.

optional arguments:
  -h, --help            show this help message and exit
  --from FROM_FMT, -f FROM_FMT
                        The input file format. Default: guess from the
                        filename extension.
  --to TO_FMT, -t TO_FMT
                        The output file format. Default: json
  --locale LOCALE, -l LOCALE
                        The locale to extract from the input document.
                        Default: all locales in the source.
  --out OUT_DIR, -o OUT_DIR
                        The directory to write to. "-" for stdout. Default:
                        src/main/resources/strings/source
Prerequisites

convert.py depends on the openpyxl library to read Microsoft Excel xlsx files. requirements.txt captures the project's dependencies. Install them to your writable user directory with:
pip install --user -r requirements.txt
Or on Windows,
py -m pip install --user -r requirements.txt
Be aware that you may have more than one version of Python installed simulataneously. Be sure you know which one is registered with the OS's drag-and-drop handler.
Input

All of these configuration details are stored in convert.ini.
The spreadsheet must have one page named "{project} Master String Set". This is defined in:
[XlsxReader]
Spreadsheet Sheet Name: Project Master String Set
There must be one column containing the human-readable string IDs:
[XlsxReader]
String ID Column Name: String ID
There must be at least one column containing the string data for a given locale. These columns may be named anything you like, but their column names must be unique. These are listed in (locale, column name) pairwise format:
[Excel Locale Columns]
en_US: String value English, US
es_MX: String value Spanish, MEXICO
...
Processing

It is an error if a row has text in the string data column, but no string ID. This is not fatal, but the row will not be written to output.
Output

Each locale column present in the Excel spreadsheet is written to a separate json file, named strings-{locale}.json. This name is configurable in convert.ini:
[JsonWriter]
File Pattern: strings-%s.json
Output files are written by default to src/main/resources/strings/source/, but this can be overridden with the --out command-line parameter.
Errors in the Excel document are written to errors.txt in the same directory as the script. errors.txt is overwritten with every run of the script.
readme file has the 
<!---
MasterLocal/MasterLocal is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
