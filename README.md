# NanaBox Config Generator

A web-based configuration file generator for [NanaBox](https://github.com/M2Team/NanaBox) `.7b` virtual machine configuration files.

🔗 **Live:** https://dmatrix68-boop.github.io/nanabox-config/

![NanaBox Config Generator](https://img.shields.io/badge/NanaBox-.7b%20Generator-00d4ff?style=for-the-badge&logo=windows&logoColor=white)

---

## Features

- **Live Preview** – JSON output with syntax highlighting updates in real time
- **Import** – Drag & drop or file picker to load existing `.7b` files, with a summary modal before applying
- **Download** – Generates UTF-8 BOM encoded `.7b` files as required by NanaBox

## Covered Configuration Sections

| Section | Fields |
|---|---|
| **Basic** | Name, GuestType, ProcessorCount, MemorySize |
| **SCSI Devices** | VirtualDisk, VirtualImage, PhysicalDevice – with file browser |
| **Network Adapters** | MAC, EndpointId, Switch (ID/Name/Subnet), Connected |
| **GPU** | AssignmentMode (Disabled/Default/Mirror/List), EnableHostDriverStore, SelectedDevices |
| **Security** | SecureBoot, TPM 2.0, ExposeVirtualizationExtensions |
| **COM Ports** | UefiConsole, ComPort1, ComPort2 |
| **State Files** | GuestStateFile *(required)*, RuntimeStateFile *(required)*, SaveStateFile |
| **Video Monitor** | HorizontalResolution, VerticalResolution, DisableBasicSessionDpiScaling |
| **Keyboard** | RedirectKeyCombinations, all 9 Virtual Key Code hotkeys |
| **Enhanced Session** | 11 redirect flags, per-drive selection (A–Z) |
| **Chipset / SMBIOS** | Manufacturer, ProductName, Version, Family, SKUNumber, SerialNumber, UUID, … |
| **Policies** | All 10 legacy/force flags (requires Windows 11 24H2+) |
| **Shares** | Plan 9 Shares, Virtual SMB Shares |

## Notes

- `GuestStateFile` and `RuntimeStateFile` are **always written** to the output – NanaBox throws a *File not found* error if they are missing. If left blank, they default to `<VM-Name>.vmgs` / `<VM-Name>.vmrs`.
- The file browser button on SCSI path fields uses the [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API) where available. Due to browser security restrictions, only the filename is populated – the full path must be completed manually.

## Reference

- [NanaBox Configuration Reference](https://github.com/M2Team/NanaBox/blob/main/Documents/ConfigurationReference.md)
- [NanaBox on GitHub](https://github.com/M2Team/NanaBox)

## License

MIT
