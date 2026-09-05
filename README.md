# NanaBox Config Generator

A web-based configuration file generator for [NanaBox](https://github.com/M2Team/NanaBox) `.7b` virtual machine configuration files.

Covers the full configuration reference as of **NanaBox 1.6 Update 5**.

🔗 **Live:** https://dmatrix68-boop.github.io/nanabox-config/

![NanaBox Config Generator](https://img.shields.io/badge/NanaBox-.7b%20Generator-00d4ff?style=for-the-badge&logo=windows&logoColor=white)

---

## Features

- **Live Preview** – JSON output with syntax highlighting updates in real time
- **Import** – Drag & drop or file picker to load existing `.7b` files, with a summary modal before applying
- **Download** – Generates UTF-8 BOM encoded `.7b` files as required by NanaBox
- **Lossless round-trip** – Imported values are preserved on export, including policies this generator does not know yet
- **Validation hints** – Warns when a share `Name` collides with an access name NanaBox reserves for `EnableHostDriverStore`

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
| **Enhanced Session** | 11 redirect flags, per-drive selection (A–Z), per-device selection (`Devices`) |
| **Chipset / SMBIOS** | Manufacturer, ProductName, Version, Family, SKUNumber, SerialNumber, UUID, … |
| **Policies** | All 10 legacy/force flags (requires Windows 11 24H2+), plus unknown policies carried over from an import |
| **Shares** | Plan 9 Shares *(1.5 Update 2)*, Virtual SMB Shares *(1.6 Update 1)* |

## Notes

- `GuestStateFile` and `RuntimeStateFile` are **always written** to the output – NanaBox throws a *File not found* error if they are missing. If left blank, they default to `<VM-Name>.vmgs` / `<VM-Name>.vmrs`.
- The file browser button on SCSI path fields uses the [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API) where available. Due to browser security restrictions, only the filename is populated – the full path must be completed manually.
- `EnhancedSession.Devices` takes **device instance paths** (e.g. `USB\VID_5986&PID_211C&MI_00\6&218C4A3&0&0000`), obtainable from Device Manager (*Details → Device instance path*) or `Get-PnpDevice`.
- With `EnableHostDriverStore` enabled, NanaBox creates read-only shares named `NanaBox.HostDrivers`, `NanaBox.HostLxssLib` and the deprecated `HostDriverStore`. Own shares must not reuse those names – the generator flags a collision.

## Reference

- [NanaBox Configuration Reference](https://github.com/M2Team/NanaBox/blob/main/Documents/ConfigurationReference.md)
- [NanaBox on GitHub](https://github.com/M2Team/NanaBox)

## License

MIT
