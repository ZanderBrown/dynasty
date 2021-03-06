dynasty
=======

A dynamic visualization tool for dynasties and other succession timelines.
Renders dynasty timelines with life, reign and, (if applicable) reign as co-monarch.

Originally built for this visualization of the reigns of the roman emperors.

![Roman emperors](examples/rome.png)

## Usage

Clone this repository and open index.html in your browser to try it locally. You'll need a local HTTP server for this to work in some browsers. In this case, if you have Python 3, just run `python3 -m http.server` and go to `localhost:8000` in your browser.

To create your own visualizations, prepare 2 CSV files following the format outlined below, and change the variables **emperor_file** and **dynasty_file** in the beginning of script.js.

You'll also want to set the other config variables, **TITLE**, **DATA_SOURCE** and **CREDIT**. If you want, you can also disable these things with the **SHOW_INFO** flag, such that only the actual visualization is rendered. If you want to disable the dynasty labels and bars as well, you can do it by setting the **SHOW_DYNASTIES** flag.

If you want the visualization as a self-contained SVG, just click the "Download as SVG" button.

## CSV files

The visualzation is generated from 2 CSV files, a list of all emperors, and a list of all dynasties. The paths to these files can be configured in the first few lines of script.js by changing the variables **emperor_file** and **dynasty_file**.

### emperor_file

name | birth | death | ascension | abdication | ascension (co-emperor) | abdication (co-emperor)
-----|-------|-------|-----------|------------|------------------------|-----------------------
string | date | date | date or **"n"** | date or **"d"** or **"n"** | date or **"n"** | date or **"a"** or **"d"** or **"n"**
`Augustus` | `23/9/-63` | `19/8/14` | `16/1/-27` | `d` | `n` | `n`
`Valerian` | `#195` | `#260_270` | `1/10/253` | `#260` | `n` | `n`
`Constantius` | `31/3/250` | `#306` | `1/5/305` | `25/7/306` | `#293` | `a`


Explanation of optional parameters:

parameter | meaning
----------|--------
**n** | not applicable (e.g. if an emperor never served as co-emperor)
**d** | abdication date same as death date (died in office)
**a** | co-emperor abdication date same as ascension date to emperor

### dynasty_file

name of the dynasty | first emperor's name | last emperor's name | display color
--------------------|----------------------|---------------------|--------------
string | string | string | hex color
`Julio-Claudians` | `Augustus` | `Nero` | `#c00465`
`Flavians` | `Vespasian` | `Domitian` | `#47c00a`
`Antonines` | `Nerva` | `Commodus` | `#bc0b0b`

## Date format

The date format is relatively complex because it has to account for incomplete historical records. Dates can be be expressed as *precise dates*, as *full years* (very common among roman emperors) and as *ranges of time*.

name | format | example | natural language
-----|--------|---------|-----------------
Exact date | `d/m/y` | `4/4/-34` | April 4, 34 BC
Full year | `#y` | `#-34` | At some point during 34 BC
Range between exact dates | `#d/m/y_d/m/y` | `#2/3/-11_12/7/19` | At some point between March 2, 11 BC and July 12, 19 AD
Range between full years | `#y_y` | `#-11_19` | At some point between January 1, 11 BC and December 31, 19 AD
Range between exact date and full year | `#d/m/y_y` | `#2/3/-11_19` | At some point between March 2, 11 BC and December 31, 19 AD
