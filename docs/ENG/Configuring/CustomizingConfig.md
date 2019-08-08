### Setup the config.plist file

Here is described how I have changed net config that goes along with Clover revision 5018.

You can download the disk image with this config from the official page of the loader Clover: https://sourceforge.net/projects/cloverefiboot/files/Bootable_ISO/ For unpacking .lzma and .tar files in Windows use [7zip](https://www.7-zip.org/) or [Bandizip]([https://bandisoft.com/bandizip](https://www.bandisoft.com/bandizip))

Here's what I changed in my file [config.plist](/CLOVER/config.plist):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>ACPI</key>
        <dict>
            <key>DSDT</key>
            <dict>
                <key>Fixes</key>
                <dict>
                    <key>AddHDMI</key>
                    <false/>
                    <key>FixDisplay</key>
                    <false/>
                </dict>
                <key>Patches</key>
                <array>
                    <dict>
                        <key>Comment</key>
                        <string>Add _SUN property for GIGE</string>
                        <key>Disabled</key>
                        <false/>
                        <key>Find</key>
                        <data>
					UFhTWAhfQURSAAhfUFJXEgYC
					</data>
                        <key>Replace</key>
                        <data>
					UFhTWAhfQURSAAhfU1VOCgQIX1BSVxIGAg==
					</data>
                    </dict>
                    <dict>
                        <key>Comment</key>
                        <string>Rename HDEF to AZAL</string>
                        <key>Disabled</key>
                        <false/>
                        <key>Find</key>
                        <data>
					SERFRg==
					</data>
                        <key>Replace</key>
                        <data>
					QVpBTA==
					</data>
                    </dict>
                    <dict>
                        <key>Comment</key>
                        <string>NVOP</string>
                        <key>Disabled</key>
                        <true/>
                        <key>Find</key>
                        <data>
					W4EOUENBUAMAQAhMQ1RMEBQfX0lOSQBwAFwv
					BV9TQl9QQ0kwUlAwNVBYU1hfQURSFEAN
					</data>
                        <key>Replace</key>
                        <data>
					W4EOUENBUAMAQAhMQ1RMEBQjX0lOSQBwAFwv
					BV9TQl9QQ0kwUlAwNVBYU1hfQURSX09GRhRA
					DQ==
					</data>
                    </dict>
                </array>
            </dict>
            <key>SSDT</key>
            <dict>
                <key>Generate</key>
                <dict>
                    <key>CStates</key>
                    <false/>
                    <key>PStates</key>
                    <false/>
                    <key>PluginType</key>
                    <true/>
                </dict>
            </dict>
        </dict>
        <key>Boot</key>
        <dict>
            <key>Arguments</key>
            <string>uia_exclude=HS07 darkwake=0</string>
            <key>HibernationFixup</key>
            <false/>
            <key>RtcHibernateAware</key>
            <true/>
            <key>Timeout</key>
            <integer>3</integer>
        </dict>
        <key>Devices</key>
        <dict>
            <key>Properties</key>
            <dict>
                <key>PciRoot(0x0)/Pci(0x2,0x0)</key>
                <dict>
                    <key>AAPL,ig-platform-id</key>
                    <data>
				AAAWGQ==
				</data>
                    <key>device-id</key>
                    <data>
				FhkAAA==
				</data>
                    <key>disable-external-gpu</key>
                    <data>
				AQAAAA==
				</data>
                    <key>framebuffer-fbmem</key>
                    <data>
				AACQAA==
				</data>
                    <key>framebuffer-patch-enable</key>
                    <data>
				AQAAAA==
				</data>
                    <key>framebuffer-stolenmem</key>
                    <data>
				AAAwAQ==
				</data>
                    <key>model</key>
                    <string>Intel HD Graphics 520</string>
                </dict>
            </dict>
            <key>Audio</key>
            <dict>
                <key>Inject</key>
                <integer>13</integer>
            </dict>
            <key>SetIntelBacklight</key>
            <true/>
        </dict>
        <key>GUI</key>
        <dict>
            <key>Hide</key>
            <array>
                <string>Preboot</string>
                <string>Recovery</string>
                <string>Legacy HD</string>
            </array>
            <key>Language</key>
            <string>ru:0</string>
            <key>Mouse</key>
            <dict>
                <key>Enabled</key>
                <true/>
                <key>Mirror</key>
                <false/>
                <key>Speed</key>
                <integer>8</integer>
            </dict>
            <key>ScreenResolution</key>
            <string>1920x1080</string>
            <key>Theme</key>
            <string>Mojave</string>
        </dict>
        <key>Graphics</key>
        <dict>
            <key>Inject</key>
            <dict>
                <key>ATI</key>
                <false/>
                <key>Intel</key>
                <false/>
                <key>NVidia</key>
                <false/>
            </dict>
        </dict>
        <key>KernelAndKextPatches</key>
        <dict>
            <key>KernelPm</key>
            <true/>
        </dict>
        <key>SMBIOS</key>
        <dict>
            <key>ProductName</key>
            <string>MacBookPro13,1</string>
        </dict>
        <key>SystemParameters</key>
        <dict>
            <key>InjectKexts</key>
            <true/>
        </dict>
    </dict>
</plist>
```

This is not a working config.plist. I brought only those items that have been modified compared to the native configuration file of the ISO image Clover revision 5033.

Such SMBIOS will be suitable for loading, but then it is better to generate its points completely, for example with the help of Clover Configurator.

Also, you should read the book "[Clover of Hacky Color](https://sourceforge.net/projects/cloverefiboot/files/Documents/)" to understand which items in config.plist responsible for what.

#### Explanations

---

The boot argument `uia_exclude=HS07` is used with the [USBInjectAll](/docs/ENG/Configuring/InstalledKexts.md) kext. I used this "bundle" to disable Bluetooth in the Hackintosh.

What to write to you instead of `HS07` you can learn using [IORegistryExplorer](/docs/ENG/ProgramsList/HackintoshTools.md), by searching for the word "bluetooth".

I needed to disable Bluetooth when additional upgrade mac OS Mojave 10.14.6, because the update [wanted to install](https://vk.com/wall-12954845_488300) due to some problems with Bluetooth. Just disabled the module will not waste battery power, which will give a small increase in autonomy.

---