# Wafer_Yield_Summary_Report

Automated KGD (Known Good Die) test data processing and yield reporting tool.

## Overview

Reads proprietary XML files from KGD test equipment, decodes them,
and generates two structured Excel reports:

| Report | Contents |
|--------|----------|
| `<WaferID>_<PartNum>_Wafer_Summary.xlsx` | Wafer Info, Test Summary, Wafer Map |
| `<WaferID>_<PartNum>_Data_Summary.xlsx`  | Per-die metadata + test parameter values |

## XML Decoding Pipeline

```
raw file -> hex string -> XOR 0xFF -> string reversal -> valid XML
```

## Features

- Drag-and-drop folder input (multi-folder supported)
- User-defined Wafer ID injected into all output fields
- Auto-scaled Wafer Map: Pass = light blue, Fail = orange
- Out-of-spec highlighting in Data Summary (red cells)
- Failure code ranking by yield impact (highest count first)
- Multi-LOT_ID guard with user alert
- Null-column filtering (e.g. vision-only steps excluded)
- Duplicate-run protection (button disabled during processing)
- Dual save paths with automatic fallback:
  - Primary: `Z:\ToFTP` + `Z:\KYEC`
  - Fallback: `C:\KGD_data\Molex_KGD_Data`

## Tech Stack

| Layer | Technology |
|-------|------------|
| Language | Python 3.x |
| Excel output | openpyxl |
| GUI | tkinter + tkinterdnd2 |
| Packaging | PyInstaller (standalone .exe) |
| Development | Cursor IDE + Claude AI |

## Quickstart

```bash
pip install openpyxl tkinterdnd2
python Wafer_Summary_Report.py
```

## Build standalone exe

Double-click `build_exe.bat` on Windows.
Installs Python if absent, builds `Wafer_Summary_Report.exe`.
