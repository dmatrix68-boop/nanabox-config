Adding a GPU device no longer means typing a device interface path by hand.

## GPU device selection

The GPU section can now read the available GPUs from the host and offer them in a dropdown.

A browser cannot enumerate the host's PCI devices — no web API exposes device interface paths — so the paths come from a PowerShell command you run on the host and paste back:

```powershell
Get-CimInstance -Namespace root\virtualization\v2 -ClassName Msvm_PartitionableGpu | Select-Object -ExpandProperty Name
```

This uses `Msvm_PartitionableGpu`, the WMI class the [NanaBox configuration reference](https://github.com/M2Team/NanaBox/blob/main/Documents/ConfigurationReference.md#selecteddevices) points at for `SelectedDevices`, so it returns exactly the paths the `List` assignment mode needs.

- The parser accepts both the plain text form and `ConvertTo-Json`, keeps only paths carrying `GPUPARAV` and drops duplicates
- Reading devices creates the first GPU entry right away, with the device pre-selected and its interface path filled in
- Every GPU entry offers the detected devices in a dropdown, labelled by vendor and device ID (`NVIDIA · DEV_2684`)
- "Add GPU device" prefills the new entry with the next device no other entry uses
- The device list is kept in the browser so it survives a reload
- The adapter your browser renders with is shown as a hint for picking the right entry — it is not a device interface path

`PartitionId` is left untouched on selection: blank makes NanaBox use GPU-PV, and the scan carries no information about whether GPU-P is wanted.

## Unchanged

Everything from v1.0.0 — full coverage of the NanaBox configuration reference as of 1.6 Update 5, the bilingual English/German interface, live JSON preview, import with preview and UTF-8 BOM encoded `.7b` output.

🔗 **Live:** https://dmatrix68-boop.github.io/nanabox-config/

**Full changelog:** https://github.com/dmatrix68-boop/nanabox-config/compare/v1.0.0...v1.1.0
