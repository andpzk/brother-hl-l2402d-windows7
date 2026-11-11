# Brother HL-L2402D on Windows 7 SP1 x64

A signed Microsoft Update Catalog driver worked with the Brother HL-L2402D connected directly by USB to Windows 7 Ultimate SP1 x64 (build 7601). Windows accepted the driver with signature enforcement enabled, created the **Brother HL-L2402D Printer** queue, and printed a physical Windows test page. [Brother's supported OS list](https://support.brother.com/g/b/oslist.aspx?c=eu_ot&lang=en&prod=hll2402d_eu) does not include Windows 7. This is a tested compatibility workaround for one setup.

## Download the exact package

[Download the original CAB from Microsoft](https://catalog.s.download.windowsupdate.com/d/msdownload/update/driver/drvs/2023/02/664d6957-9627-4799-ad16-1a2f1ef2c52c_fc36b9dd76f66e7d54a44586486c7233ed535f1f.cab) and save it as <code>Brother-HL-L2402D-1.0.0.0.cab</code>. The driver remains hosted by Microsoft.

- [Microsoft Update Catalog entry](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=32d7d897-6a94-43c7-abdf-8a5ae5449023) — Brother - Printer - 1.0.0.0
- Driver INF — <code>BROHL22A.INF</code>
- Matching USB printer hardware ID — <code>USBPRINT\BROTHERHL-L2402D5E4C</code>
- SHA-256 — <code>177924E478572555C23A3945C8E90B9ABF9016FF1B64DBB34B09AAFBCA999D63</code>

## Install or reinstall

1. On Windows 7 SP1 x64, check that [Microsoft's SHA-2 code-signing support (KB4474419)](https://support.microsoft.com/help/4474419) is installed. The tested PC already had this update.
2. Copy the CAB into a new folder on the Windows 7 PC. Connect the printer by USB and turn it on.
3. Open **Command Prompt** as administrator and change to the new folder. Check the CAB hash and compare it with the full SHA-256 above.

   ~~~cmd
   certutil -hashfile "Brother-HL-L2402D-1.0.0.0.cab" SHA256
   ~~~

4. If the checksum matches, extract the CAB and install the INF using Windows' built-in tools. Keep the extracted files together. If Windows rejects the package, stop and record the error. Keep driver signature enforcement enabled.

   ~~~cmd
   mkdir extracted
   expand -F:* "Brother-HL-L2402D-1.0.0.0.cab" extracted
   pnputil -i -a "extracted\BROHL22A.INF"
   ~~~

5. Open **Control Panel > Devices and Printers**. Right-click **Brother HL-L2402D Printer**, select **Printer properties**, then **Print Test Page**. To make it the default for your account, right-click the printer and select **Set as default printer**.
