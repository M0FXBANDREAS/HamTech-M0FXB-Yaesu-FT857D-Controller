# HamTech M0FXB Yaesu FT857D Controller

Windows 10/11 desktop CAT controller adapted specifically for the Yaesu FT-857D.

## Supported documented CAT controls
- Read/set frequency (10 Hz CAT resolution)
- LSB, USB, CW, CWR, AM, WFM, FM, DIG and PKT modes
- VFO A/B toggle
- Split on/off
- Clarifier/RIT
- PTT press-and-hold
- RX S-meter/status polling
- Repeater shift and offset
- CTCSS encoder and tone
- 50 application-side named memories

The FT-857D operating manual documents the five-byte CAT protocol used for these controls. Direct EEPROM/internal-memory access from the old FT-817/818 project is deliberately disabled because the FT-817/818 hard-coded EEPROM map is not documented for the FT-857D.

## Run
Extract the ZIP and double-click `START-HAMTECH-FT857D-CONTROLLER.cmd`.
On first run it requires the free .NET 8 SDK to build a self-contained Windows x64 executable. The result is `publish\HamTech-M0FXB-FT857D-Controller.exe`.

Connect a suitable FT-857D TTL CAT interface to the radio's CAT/LINEAR jack. Set Menu 020 [CAT/LIN/TUN] to CAT, set Menu 019 [CAT RATE] to 4800, 9600 or 38400, then select the matching COM port and baud rate in the controller. CAT framing is 8 data bits, no parity, 2 stop bits.

## Safety
Test in Demo mode first. PTT is press-and-hold. Verify antenna, frequency, mode, licence privileges and station configuration before transmitting.

Independent project; not affiliated with or endorsed by Yaesu. Yaesu and FT-857D are trademarks of their respective owner.


## V2 display and memory changes

- 16-segment LCD S-meter: S0-S9 illuminate green; S9+10 through +60 illuminate red.
- 200 controller-side named memories, shown as M-001 through M-200. The selected controller memory name is shown on the LCD panel when recalled.
- PC squelch remains an audio mute threshold driven by the CAT S-meter.
- RF Gain remains a radio-front-panel control because the documented FT-857D CAT opcode table does not provide a continuous RF Gain command.
- Direct EEPROM memory reads are removed. Standard FT-857D CAT does not document a command for reading stored alpha tags, so this build does not guess EEPROM addresses.


## V3 radio-status display

V3 adds FT-857D documented F7 TX-status polling. The main segmented meter automatically shows receive S-meter data in RX and PO meter data in TX, including TX/RX detection from the radio, SPLIT state and a prominent HI-SWR warning. No numerical SWR/ALC value is invented because the documented CAT status byte does not provide one.

## V4 visual / tuner controls
- More realistic FT-857D-inspired MAIN DIAL with concentric grip rings and index marker.
- Reworked cream-face analogue S/PO meter with denser scale, green S range and red strong-signal range.
- F11 toggles true borderless full-screen mode; Esc restores the window.
- Orange TUNER button provides the correct FC-30/ATAS setup workflow. The FT-857D rear CAT/LINEAR jack is shared with tuner control, so an FC-30 cannot be commanded through that socket while this app remains connected by CAT. No undocumented tuner CAT opcode is sent.
