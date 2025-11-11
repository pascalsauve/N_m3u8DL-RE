# N_m3u8DL-RE
A cross-platform DASH/HLS/MSS download tool. Supports VOD and live streaming (DASH/HLS).

[![img](https://img.shields.io/github/stars/nilaoda/N_m3u8DL-RE?label=Stars)](https://github.com/nilaoda/N_m3u8DL-RE)  [![img](https://img.shields.io/github/last-commit/nilaoda/N_m3u8DL-RE?label=Last%20Commit)](https://github.com/nilaoda/N_m3u8DL-RE)  [![img](https://img.shields.io/github/release/nilaoda/N_m3u8DL-RE?label=Latest%20Release)](https://github.com/nilaoda/N_m3u8DL-RE/releases)  [![img](https://img.shields.io/github/license/nilaoda/N_m3u8DL-RE?label=License)](https://github.com/nilaoda/N_m3u8DL-RE)   [![img](https://img.shields.io/github/downloads/nilaoda/N_m3u8DL-RE/total?label=Downloads)](https://github.com/nilaoda/N_m3u8DL-RE/releases)


If you encounter a bug, please first confirm whether the software is the latest version (if using the Release version, it is recommended to download the latest auto-built version from the [Actions](https://github.com/nilaoda/N_m3u8DL-RE/actions) page and check if the issue has been fixed). If the version is up-to-date and the issue persists, you can check [Issues](https://github.com/nilaoda/N_m3u8DL-RE/issues) to see if someone else has encountered a similar problem. If not, feel free to ask.

---

Older versions of Windows' built-in terminal may not support this program. Alternative: Run it in [cmder](https://github.com/cmderdev/cmder).

Arch Linux users can install it from AUR: [n-m3u8dl-re-bin](https://aur.archlinux.org/packages/n-m3u8dl-re-bin), [n-m3u8dl-re-git](https://aur.archlinux.org/packages/n-m3u8dl-re-git)

```bash
# Install N_m3u8DL-RE release version on Arch Linux and derivatives (not maintained by the author)
yay -Syu n-m3u8dl-re-bin

# Install N_m3u8DL-RE development version on Arch Linux and derivatives (not maintained by the author)
yay -Syu n-m3u8dl-re-git
```
---

# Command Line Parameters
```
Description:
  N_m3u8DL-RE (Beta version) 20251027

Usage:
  N_m3u8DL-RE <input> [options]

Arguments:
  <input>  URL or file

Options:
  --tmp-dir <tmp-dir>                                     Set temporary file storage directory
  --save-dir <save-dir>                                   Set output directory
  --save-name <save-name>                                 Set output file name
  --save-pattern <save-pattern>                           Set output file naming template, supports variables: 
                                                          <SaveName>, <Id>, <Codecs>, <Language>, <Resolution>, 
                                                          <Bandwidth>, <MediaType>, <Channels>, <FrameRate>, 
                                                          <VideoRange>, <GroupId>, <Ext>
                                                          Example: --save-pattern "<SaveName>_<Resolution>_<Bandwidth>"
  --log-file-path <log-file-path>                         Set log file path, e.g., C:\Logs\log.txt
  --base-url <base-url>                                   Set BaseURL
  --thread-count <number>                                 Set download thread count [default: CPU thread count]
  --download-retry-count <number>                         Retry count for each segment download error [default: 3]
  --http-request-timeout <seconds>                        HTTP request timeout in seconds [default: 100]
  --force-ansi-console                                    Force terminal to support ANSI and be interactive
  --no-ansi-color                                         Remove ANSI colors
  --auto-select                                           Automatically select the best track of all types [default: False]
  --skip-merge                                            Skip segment merging [default: False]
  --skip-download                                         Skip downloading [default: False]
  --check-segments-count                                  Check if the actual downloaded segment count matches the expected count [default: True]
  --binary-merge                                          Binary merge [default: False]
  --use-ffmpeg-concat-demuxer                             Use ffmpeg concat demuxer instead of concat protocol for merging [default: False]
  --del-after-done                                        Delete temporary files after completion [default: True]
  --no-date-info                                          Do not write date info during muxing [default: False]
  --no-log                                                Disable log file output [default: False]
  --write-meta-json                                       Output parsed information as a JSON file [default: True]
  --append-url-params                                     Append URL parameters to segments, useful for some websites like kakao.com [default: False]
  -mt, --concurrent-download                              Concurrently download selected audio, video, and subtitles [default: False]
  -H, --header <header>                                   Set specific HTTP request headers, e.g.:
                                                          -H "Cookie: mycookie" -H "User-Agent: iOS"
  --sub-only                                              Select subtitle tracks only [default: False]
  --sub-format <SRT|VTT>                                  Subtitle output format [default: SRT]
  --auto-subtitle-fix                                     Automatically fix subtitles [default: True]
  --ffmpeg-binary-path <PATH>                             Full path to ffmpeg executable, e.g., C:\Tools\ffmpeg.exe
  --log-level <DEBUG|ERROR|INFO|OFF|WARN>                 Set log level [default: INFO]
  --ui-language <en-US|zh-CN|zh-TW>                       Set UI language
  --urlprocessor-args <urlprocessor-args>                 Pass this string directly to the URL Processor
  --key <key>                                             Set decryption key. The program uses mp4decrypt/shaka-packager/ffmpeg for decryption. Format:
                                                          --key KID1:KEY1 --key KID2:KEY2
                                                          For identical keys, you can directly input --key KEY
  --key-text-file <key-text-file>                         Set key file. The program will search for the KEY by KID in the file for decryption (large files not recommended)
  --decryption-engine <FFMPEG|MP4DECRYPT|SHAKA_PACKAGER>  Set the third-party program for decryption [default: MP4DECRYPT]
  --decryption-binary-path <PATH>                         Full path to the MP4 decryption tool, e.g., C:\Tools\mp4decrypt.exe
  --mp4-real-time-decryption                              Real-time decryption of MP4 segments [default: False]
  -R, --max-speed <SPEED>                                 Set speed limit, supports Mbps or Kbps, e.g., 15M 100K
  -M, --mux-after-done <OPTIONS>                          Attempt to mux audio and video after all tasks are completed. Enter "--morehelp mux-after-done" for details
  --custom-hls-method <METHOD>                            Specify HLS encryption method (AES_128|AES_128_ECB|CENC|CHACHA20|NONE|SAMPLE_AES|SAMPLE_AES_CTR|UNKNOWN)
  --custom-hls-key <FILE|HEX|BASE64>                      Specify HLS decryption key. Can be a file, HEX, or Base64
  --custom-hls-iv <FILE|HEX|BASE64>                       Specify HLS decryption IV. Can be a file, HEX, or Base64
  --use-system-proxy                                      Use system default proxy [default: True]
  --custom-proxy <URL>                                    Set request proxy, e.g., http://127.0.0.1:8888
  --custom-range <RANGE>                                  Download only specific segments. Enter "--morehelp custom-range" for details
  --task-start-at <yyyyMMddHHmmss>                        Do not start the task before this time
  --live-perform-as-vod                                   Download live streams as VOD [default: False]
  --live-real-time-merge                                  Real-time merge during live recording [default: False]
  --live-keep-segments                                    Keep segments even when real-time merging is enabled during live recording [default: True]
  --live-pipe-mux                                         Use pipe + ffmpeg for real-time muxing to TS files during live recording with real-time merging [default: False]
  --live-fix-vtt-by-audio                                 Fix VTT subtitles by reading the start time of the audio file [default: False]
  --live-record-limit <HH:mm:ss>                          Set recording duration limit for live streams
  --live-wait-time <SEC>                                  Manually set live playlist refresh interval
  --live-take-count <NUM>                                 Manually set the number of segments to fetch initially during live recording [default: 16]
  --mux-import <OPTIONS>                                  Import external media files during muxing. Enter "--morehelp mux-import" for details
  -sv, --select-video <OPTIONS>                           Select video streams matching the criteria using regex. Enter "--morehelp select-video" for details
  -sa, --select-audio <OPTIONS>                           Select audio streams matching the criteria using regex. Enter "--morehelp select-audio" for details
  -ss, --select-subtitle <OPTIONS>                        Select subtitle streams matching the criteria using regex. Enter "--morehelp select-subtitle" for details
  -dv, --drop-video <OPTIONS>                             Drop video streams matching the criteria using regex
  -da, --drop-audio <OPTIONS>                             Drop audio streams matching the criteria using regex
  -ds, --drop-subtitle <OPTIONS>                          Drop subtitle streams matching the criteria using regex
  --ad-keyword <REG>                                      Set URL keyword (regex) for ad segments
  --disable-update-check                                  Disable version update check [default: False]
  --allow-hls-multi-ext-map                               Allow multiple #EXT-X-MAP in HLS (experimental) [default: False]
  --morehelp <OPTION>                                     View detailed help for a specific option
  -?, -h, --help                                          Show help and usage information
  --version                                               Show version information
```

<details>
<summary>Click to view More Help</summary> 

```
More Help:

  --mux-after-done

Attempt to mux audio and video after all tasks are completed. You can specify the following parameters separated by colons:

* format=FORMAT: Specify the container (mkv, mp4)
* muxer=MUXER: Specify the muxing program (ffmpeg, mkvmerge) (default: ffmpeg)
* bin_path=PATH: Specify the program path (default: auto-detect)
* skip_sub=BOOL: Whether to ignore subtitle files (default: false)
* keep=BOOL: Whether to keep files after muxing (true, false) (default: false)

Examples:
# Mux to mp4 container
-M format=mp4
# Use mkvmerge, auto-detect program
-M format=mkv:muxer=mkvmerge
# Use mkvmerge, custom program path
-M format=mkv:muxer=mkvmerge:bin_path="C\:\Program Files\MKVToolNix\mkvmerge.exe"
```
```
More Help:

  --mux-import

Import external media files during muxing. You can specify the following parameters separated by colons:

* path=PATH: Specify the media file path
* lang=CODE: Specify the media file language code (optional)
* name=NAME: Specify the media file description (optional)

Examples:
# Import external subtitle
--mux-import path=zh-Hans.srt:lang=chi:name="Chinese (Simplified)"
# Import external audio + subtitle
--mux-import path="D\:\media\atmos.m4a":lang=eng:name="English Description Audio" --mux-import path="D\:\media\eng.vtt":lang=eng:name="English (Description)"
--mux-import path="D\:\media\atmos.m4a":lang=eng:name="English Description Audio" --mux-import path="D\:\media\eng.vtt":lang=eng:name="English (Description)"
```
```
More Help:

  --select-video

Select video streams that match criteria via regular expressions. You can specify the following parameters separated by colons:

id=REGEX:lang=REGEX:name=REGEX:codecs=REGEX:res=REGEX:frame=REGEX
segsMin=number:segsMax=number:ch=REGEX:range=REGEX:url=REGEX
plistDurMin=hms:plistDurMax=hms:for=FOR

* for=FOR: Selection mode. best[number], worst[number], all (default: best)

Examples:
# Select the best video
-sv best
# Select 4K + HEVC video
-sv res="3840*":codecs=hvc1:for=best
# Select video with length greater than 1 hour 20 minutes 30 seconds
-sv plistDurMin="1h20m30s":for=best
```
```
More Help:

  --select-audio

Select audio streams that match criteria via regular expressions. Refer to --select-video.

Examples:
# Select all audio
-sa all
# Select the best English track
-sa lang=en:for=best
# Select the best two English (or Japanese) tracks
-sa lang="ja|en":for=best2
```
```
More Help:

  --select-subtitle

Select subtitle streams that match criteria via regular expressions. Refer to --select-video.

Examples:
# Select all subtitles
-ss all
# Select all subtitles whose name contains "Chinese"
-ss name="Chinese":for=all
```
```
More Help:

  --custom-range

When downloading VOD content, download only a subset of segments.

Examples:
# Download 11 segments [0,10]
--custom-range 0-10
# Download segments starting from index 10
--custom-range 10-
# Download the first 100 segments
--custom-range -99
# Download from minute 5 to minute 20
--custom-range 05:00-20:00
```
```
More Help:

  --save-pattern

Use variables to set the output file naming template. Supported variables:

* <SaveName>: User-specified save name (--save-name)
* <Id>: Task ID of the stream
* <Codecs>: Codec information (e.g., avc1.64001f, mp4a.40.2)
* <Language>: Language code (e.g., en, zh-CN)
* <Resolution>: Video resolution (e.g., 1920x1080)
* <Bandwidth>: Stream bandwidth/bitrate
* <MediaType>: Media type (VIDEO, AUDIO, SUBTITLES)
* <Channels>: Audio channel configuration
* <FrameRate>: Frame rate
* <VideoRange>: Video color gamut/HDR information (SDR, HDR10, etc.)
* <GroupId>: Stream group identifier

Use cases:
When downloading multiple streams of the same type (e.g., multiple videos at different resolutions), this option helps avoid filename conflicts.

Examples:
# Download 1080p and 720p videos, include resolution in filename
--save-pattern "<SaveName>_<Resolution>" --save-name "video"
# Output: video_1920x1080.mp4, video_1280x720.mp4

# Include bandwidth information
--save-pattern "<SaveName>_<Resolution>_<Bandwidth>kbps"
# Output: video_1920x1080_5000000kbps.mp4

# Download multiple audio streams, include language and channels
--save-pattern "<SaveName>_<Language>_<Channels>ch"
# Output: audio_en_2ch.m4a, audio_es_2ch.m4a, audio_en_6ch.m4a

# Complex template
--save-pattern "<MediaType>_<Resolution>_<Codecs>_<Language>"
# Output: VIDEO_1920x1080_avc1.64001f_en.mp4

Notes:
If --save-pattern is not used, the program will automatically generate unique filenames using the stream metadata (resolution, bandwidth, etc.) when conflicts occur, rather than simply appending a ".copy" suffix.
```
</details>



# Screenshots

## VOD

![RE1](img/RE.gif)

You can also download in parallel and auto-mux.


![RE2](img/RE2.gif)

## Live

Record TS live source:

[click to show gif](http://pan.iqiyi.com/file/paopao/W0LfmaMRvuA--uCdOpZ1cldM5JCVhMfIm7KFqr4oKCz80jLn0bBb-9PWmeCFZ-qHpAaQydQ1zk-CHYT_UbRLtw.gif)

Record MPD live source:

[click to show gif](http://pan.iqiyi.com/file/paopao/nmAV5MOh0yIyHhnxdgM_6th_p2nqrFsM4k-o3cUPwUa8Eh8QOU4uyPkLa_BlBrMa3GBnKWSk8rOaUwbsjKN14g.gif)

During recording, use ffmpeg to perform real-time muxing of audio and video:
```
ffmpeg -readrate 1 -i 2022-09-21_19-54-42_V.mp4 -i 2022-09-21_19-54-42_V.chi.m4a -c copy 2022-09-21_19-54-42_V.ts
```
In newer versions (>=v0.1.5), you can enable `live-pipe-mux` to replace the above command.

**Important:** If your network environment is unstable, do **not** enable `live-pipe-mux`. Data reading inside the pipe is handled by ffmpeg, and in some environments live data may be lost.

In newer versions (>=v0.1.8), you can modify certain ffmpeg options used by `live-pipe-mux` by setting the environment variable `RE_LIVE_PIPE_OPTIONS`: https://github.com/nilaoda/N_m3u8DL-RE/issues/162#issuecomment-1592462532

## Sponsor

<a href="https://www.buymeacoffee.com/nilaoda" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>