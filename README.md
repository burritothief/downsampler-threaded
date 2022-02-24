#### Name:
downsampler-threaded - A multi-process sox frontend for automatically resampling FLAC files.

#### Synopsis:
`downsampler-threaded.sh [OPTION [ARGUMENT]]... [--] FILE_OR_FOLDER [FILE_OR_FOLDER]...`

#### Description:
Automatically resamples 24 bit FLAC files to 16 bit and a common multiple of their sample rate.

Uses SoX with per-file multi-threading when "env_parallel", part of GNU Parallel, is detected, or with a single thread when it isn't.

Additional, optional functionality includes:
- Using 24 bit outputs (24/88.2 and 24/96) for 176.4 and 192 KHz sources
- Dithering 24/44.1 and 24/48 sources to 16 bit without resampling (or ignoring these sources)
- Using metaflac to:
   - Add padding
   - Add a SOURCE_FFP tag containing the source file's FLAC fingerprint
   - Add a SOURCE_SPECS tag containing the source file's bit depth and sample rate
   - Add a SOX_COMMAND tag containing the SoX command used to create the file

#### Depends:
Bash, sox, basename, cat, dirname, sort (-z, -u)

#### Recommends:
- Bash v4+ (globstar) -OR- a "find" command featuring the "-print0" option
   - only required to use "recurse_all_subdirs" feature
- env_parallel (and env_parallel.bash) (part of GNU Parallel)
   - required for multi-threaded operation
- realpath from GNU coreutils
   - realpath is strongly recommended, but there is a fallback Bash-function
   - if your non-GNU realpath outputs absolute paths when called with no options it should work fine
   - "grealpath" binaries will be detected and used if they are in the $PATH
- metaflac
   - only required for the optional features which use it: adding tags and padding

#### Documentation:
`-h | -H | --help`   Print full help text.
