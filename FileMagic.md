# Transmogrification of file names and contents

  * If an input file is in gzip format, it is silently unzipped.
  * An input file named "-" means "stdin"
  * An output file named "-" means "stdout"
  * An output file named "--" means "stderr"
  * An input file name starting with "<<" is a virtual file containing everything after these first two characters. Tabs, newlines and such can be backslash escaped, e.g `-f "<<four\tfive\tsix\n"` is a three column file with a newline.


## Future Plans

* Input files starting with "<" are opened with "popen"
* Output files starting with ">" are opened with "popen"
* Input files starting with "s3://" are read from AWS's S3 file system
* Input files starting with "http://" or "https://" are fetched from the live web
* ...
