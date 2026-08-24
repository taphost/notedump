# Interfacce Embedded

## 1. UART (Seriale Debug)
| Caratteristica | Dettaglio |
|---|---|
| Voltaggio | 3.3V / 5V (TTL standard) |
| Livello logico | TTL (NON RS-232, che usa ±12V) |
| Pin tipici | GND, TX, RX, VCC |
| Baud rate tipici | 115200 8N1, 57600, 38400, 9600 |
| Protocollo | Seriale asincrona |
| Accesso a | Bootloader, BusyBox, kernel log, console |
| Note | Porta più comune per debug |

**Identificazione TX:**
- Misura con multimetro: TX ~3.3V a riposo, RX ~0V
- Logic analyzer: rileva baud rate automaticamente
- Oscilla durante boot anche senza RX connesso

---

## 2. JTAG
| Caratteristica | Dettaglio |
|---|---|
| Standard | IEEE 1149.1 |
| Voltaggio | 1.8V / 2.5V / 3.3V / 5V |
| Pin principali | TDI, TDO, TCK, TMS, TRST, SRST, GND, **VREF** |
| Funzioni | Debug CPU, lettura RAM, dump flash, boundary scan |
| Boundary scan | Test connessioni hardware senza accesso CPU |
| Note | Può essere disabilitato via eFuse o secure boot |

**⚠️ VREF è critico:** Permette all'adapter di adattarsi al voltaggio target.

**Connettori comuni:**
- 20-pin ARM JTAG
- 14-pin Xilinx
- 10-pin Cortex Debug (0.05" pitch)

---

## 3. SWD (Serial Wire Debug - ARM)
| Caratteristica | Dettaglio |
|---|---|
| Tipo | Debug ARM Cortex-M/Cortex-A |
| Pin | SWDIO, SWCLK, NRST, GND, VREF |
| Voltaggio | 1.8–3.3V |
| Funzioni | Flash MCU, stepping, registri, breakpoint |
| Vantaggi | Solo 2 pin dati vs 4+ di JTAG |

**Nota:** SWD è proprietario ARM, non funziona su MIPS/RISC-V.

---

## 4. SPI Flash
| Caratteristica | Dettaglio |
|---|---|
| Voltaggio | 3.3V (1.8V su alcuni chip moderni) |
| Pin | MISO, MOSI, CLK, CS (chip select) |
| Contenuto | Bootloader, kernel, rootfs, U-Boot env |
| Dimensioni tipiche | 8MB–128MB (NOR flash) |
| Tool software | flashrom, serprog, esptool |
| Programmer HW | CH341A, TL866, Bus Pirate, FT2232H |

**Estrazione in-circuit:**
- SOIC8/SOIC16 clip + CH341A programmer
- Attenzione: alcuni SoC tengono la flash attiva (desolder o disconnetti CS)

---

## 5. I²C / EEPROM
| Caratteristica | Dettaglio |
|---|---|
| Pin | SDA, SCL, GND, VCC |
| Voltaggio | 3.3V / 5V |
| Funzione | Configurazioni, MAC address, calibrazioni |
| Tool | i2cdetect, i2cdump, Bus Pirate |
| Chip tipici | 24C02, 24C32, AT24C256 |

**Identificazione:**
- Cerca chip 8-pin vicino a Ethernet PHY o WiFi
- Serigrafie: U2, EEPROM, 24Cxx

---

## 6. Modalità USB Proprietarie (Recovery/Flash)
| SoC | Modalità | Tool | Trigger |
|---|---|---|---|
| Amlogic | USB Burning Tool | Amlogic Tool | Pulsante Update + boot |
| Rockchip | MaskROM | rkdeveloptool | RECOVERY button + USB |
| MediaTek | Preloader Mode | SP Flash Tool | Vol+ durante boot |
| Qualcomm | EDL (9008) | QPST, QFIL | Testpoint + USB |
| Broadcom | CFE Recovery | TFTP | Boot con IP 192.168.1.1 |

---

## 7. Ethernet PHY (MDIO/MDC)
| Caratteristica | Dettaglio |
|---|---|
| Funzione | Config/debug del PHY layer |
| Protocollo | MDIO (Management Data I/O) |
| Pin | MDC (clock), MDIO (data) |
| Note | Non dà accesso diretto al firmware SoC |
| Uso | Diagnostica link, modalità test |

---

## 8. GPIO di Boot / Test Mode
Alcuni SoC entrano in modalità speciali con GPIO specifici:

- **Boot da USB** invece di flash
- **Boot da UART** (Xmodem/Ymodem upload)
- **MaskROM mode** (Rockchip)
- **FEL mode** (Allwinner)
- **Disable secure boot** (solo chip senza eFuse)

**Metodo:** Collega GPIO a GND durante power-on, poi rilascia.

---

## 9. eFuse / OTP (One-Time Programmable)
| Informazione | Dettaglio |
|---|---|
| Tipo | Celle programmabili una sola volta |
| Contenuto | Chiavi secure boot, serial number, MAC, lock bit |
| Rischio | **Non riprogrammabili** - brick permanente se errore |
| Dump | Possibile via JTAG (se non bloccato) |

**⚠️ eFuse blow = irreversibile.** Mai scrivere senza backup.

---

## 10. Struttura Tipica Firmware
| Sezione | Contenuto | Formato |
|---|---|---|
| Bootloader primario | U-Boot, CFE, Barebox | Raw binary |
| Device Tree Blob | Descrizione hardware (ARM/MIPS) | .dtb |
| Kernel | Linux compresso | zImage, uImage |
| Initramfs | Mini rootfs in RAM | CPIO.gz |
| Rootfs | Sistema principale | SquashFS, UBIFS, ext4 |
| Overlay | Config persistente | JFFS2, F2FS |

---

## Bootloader Più Comuni
| Bootloader | Caratteristiche | Chip tipici |
|---|---|---|
| U-Boot | Standard de facto, scripting, TFTP/USB | ARM, MIPS, PowerPC |
| CFE | Broadcom routers | BCM47xx, BCM63xx |
| Barebox | Evoluzione moderna U-Boot | ARM, x86 |
| RedBoot | Legacy industriale | ARM7, ARM9 |
| Rockchip miniloader | Proprietario | RK3xxx |

---

## Protocolli Bootloader per Flashing
| Bootloader | Protocollo | Comando esempio |
|---|---|---|
| U-Boot | TFTP | `tftp 0x80000000 uImage; bootm` |
| U-Boot | USB | `ums 0 mmc 0` (USB Mass Storage) |
| U-Boot | Xmodem | `loady; erase; cp.b` |
| CFE | TFTP | Boot con 192.168.1.1, upload via TFTP |
| Rockchip | rkdeveloptool | `rkdeveloptool wl 0x0 boot.img` |
| Amlogic | USB Burning | GUI tool proprietario |

**U-Boot scripting:**
```bash
setenv bootcmd 'tftp 0x80000000 uImage; bootm'
saveenv
```

---

## File System Embedded
| FS | Tipo | Caratteristiche | Flash type |
|---|---|---|---|
| SquashFS | RO | Alta compressione, veloce | NOR, NAND, eMMC |
| JFFS2 | RW | Wear leveling, compress | NOR |
| UBIFS | RW | UBI layer, robusto | NAND, eMMC |
| YAFFS2 | RW | Storico, deprecato | NAND |
| cramfs | RO | Legacy, low RAM | NOR |
| Ext4 | RW | Standard Linux | eMMC, SD |
| Initramfs | RAM | Micro rootfs boot | RAM |
| F2FS | RW | Ottimizzato per flash | eMMC, SD |

---

## Tool Essenziali
| Tool | Funzione | Comando base |
|---|---|---|
| **binwalk** | Analisi firmware, estrazione | `binwalk -e firmware.bin` |
| **dd** | Estrazione raw partition | `dd if=flash.bin of=rootfs.bin bs=1 skip=0x200000` |
| **unsquashfs** | Estrai SquashFS | `unsquashfs rootfs.squashfs` |
| **jefferson** | Estrai JFFS2 | `jefferson rootfs.jffs2 -d output/` |
| **ubi_reader** | Legge UBIFS/UBI | `ubireader_extract_images firmware.bin` |
| **flashrom** | Programma SPI flash | `flashrom -p ch341a_spi -r dump.bin` |
| **openocd** | JTAG/SWD debug | `openocd -f interface/jlink.cfg` |
| **firmware-mod-kit** | Unpack/repack firmware | `extract-firmware.sh firmware.bin` |
| **sasquatch** | SquashFS varianti custom | `sasquatch rootfs.squashfs` |

---

## Programmer Hardware
| Dispositivo | Interfacce | Costo | Note |
|---|---|---|---|
| CH341A | SPI, I²C | ~5€ | Popolare, SOIC8 clip incluso |
| Bus Pirate | SPI, I²C, UART, JTAG | ~30€ | Versatile, logic analyzer |
| FT2232H | SPI, I²C, JTAG | ~15€ | Veloce, supporto flashrom |
| TL866 II Plus | Solo offline (chip desolderato) | ~50€ | Supporta molti chip |
| J-Link | JTAG, SWD | €60-500 | Professionale ARM |
| ST-Link V2 | SWD (STM32) | ~10€ | Cloni economici disponibili |

---

## Come Riconoscere UART
1. **Visivo:** 3-4 pad/pin in fila
2. **Serigrafie:** UART, TX, RX, DBG, JP1, CON1, CONSOLE
3. **Multimetro (continuità):**
   - Trova GND (continuità con ground plane)
   - TX: ~3.3V a riposo (HIGH)
   - RX: ~0V o fluttuante
4. **Logic analyzer:** Cattura segnale durante boot
5. **Prova TX:** Collega solo GND + RX del tuo adapter a ogni pad

---

## Come Riconoscere JTAG/SWD
1. **Header:** 7–20 pin (10-pin e 20-pin più comuni)
2. **Serigrafie:** TDI, TDO, TCK, TMS, SWDIO, SWCLK, JTAG, DEBUG
3. **Pattern:** Pin alternati GND per ridurre noise
4. **Test:** 
   - JTAG: `openocd -f interface/jlink.cfg -c "adapter speed 1000" -c "jtag_scan"`
   - SWD: J-Link commander, `connect`

---

## Riepilogo Livelli di Accesso
| Interfaccia | Livello accesso | Difficoltà | Rischio brick |
|---|---|---|---|
| UART | Shell/console | Basso | Basso |
| JTAG/SWD | CPU+RAM+flash | Medio | Medio |
| SPI programmer | Diretto flash chip | Alto | Alto (bad flash = brick) |
| USB MaskROM | Bootrom SoC | Basso | Basso |
| I²C EEPROM | Config/MAC | Basso | Basso |

---

## Sicurezza: Bypass e Limitazioni
| Protezione | Bypass possibile? | Metodo |
|---|---|---|
| UART disabled | ✅ Spesso | Header fisico esiste ancora |
| JTAG fuse blown | ❌ No | Hardware permanente |
| Secure boot | ⚠️ Dipende | Exploit bootloader, glitching |
| Encrypted flash | ❌ Difficile | Serve chiave (in eFuse o TEE) |
| Debug port disabled | ✅ A volte | Glitching, GPIO boot mode |

---

## Voltage Reference Quick Table
| Voltaggio | Dispositivi tipici |
|---|---|
| 5V | Arduino, vecchi UART/JTAG, alcuni Atmel |
| 3.3V | **La maggioranza** (ARM, MIPS, ESP32, routers) |
| 2.5V | Alcuni FPGA Xilinx, CPU industriali |
| 1.8V | SoC moderni (Rockchip, Qualcomm, SPI flash DDR) |

**⚠️ Mai collegare 5V a pin 1.8V = brick immediato.**

---

## Checklist Pre-Exploit
- [ ] Identificato voltaggio (multimetro)
- [ ] Backup flash originale (SPI dump o TFTP)
- [ ] Verificato pinout (TX/RX non invertiti)
- [ ] Testato con adapter USB-TTL sicuro (con isolamento)
- [ ] Documentato serigrafie e posizione componenti
- [ ] Preparato cavo UART con jumper removibili
- [ ] Annotato eventuale password bootloader

---

## Link Utili
- OpenWrt ToH (Table of Hardware): dispositivi supportati
- DeviceTree.org: sintassi DTB
- Binwalk signature database: formati firmware
- OpenOCD supported devices
- Flashrom chip database

---