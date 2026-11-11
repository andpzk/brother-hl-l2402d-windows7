# Brother HL-L2402D on Windows 7 SP1 x64

1. Connect the printer by USB and turn it on. Windows 7 needs [SHA-2 support (KB4474419)](https://support.microsoft.com/help/4474419).
2. [Download the signed driver CAB from Microsoft](https://catalog.s.download.windowsupdate.com/d/msdownload/update/driver/drvs/2023/02/664d6957-9627-4799-ad16-1a2f1ef2c52c_fc36b9dd76f66e7d54a44586486c7233ed535f1f.cab). Create a new folder called <code>C:\BrotherDriver</code> and save the file there as <code>Brother-HL-L2402D.cab</code>.
3. Open **Command Prompt as administrator**. Run:

   ~~~cmd
   cd /d C:\BrotherDriver
   certutil -hashfile Brother-HL-L2402D.cab SHA256
   ~~~

   Continue only if the hash matches <code>177924E478572555C23A3945C8E90B9ABF9016FF1B64DBB34B09AAFBCA999D63</code>.

4. Extract and install the driver:

   ~~~cmd
   mkdir extracted
   expand -F:* Brother-HL-L2402D.cab extracted
   pnputil -i -a extracted\BROHL22A.INF
   ~~~

   If Windows rejects the driver, stop. Keep signature enforcement enabled.

5. Open **Control Panel → Devices and Printers**. Right-click **Brother HL-L2402D Printer → Printer properties → Print Test Page**.

**Expected result:** Windows adds the Brother printer, and one test page prints. This was confirmed on Windows 7 Ultimate SP1 x64 over USB. [Brother does not officially list Windows 7 for this model.](https://support.brother.com/g/b/oslist.aspx?c=eu_ot&lang=en&prod=hll2402d_eu)
