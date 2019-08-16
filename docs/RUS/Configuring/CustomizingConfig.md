### Настройка файла config.plist

Здесь описано то, как я изменил чистый конфиг, который идет вместе с Clover ревизии 5033.

Вы можете скачать образ диска с данным конфигом с официальной страницы загрузчика Clover: https://sourceforge.net/projects/cloverefiboot/files/Bootable_ISO/ Для распаковки .lzma и .tar файлов в Windows лучше используйте [7zip](https://www.7-zip.org/) или [Bandizip]([https://bandisoft.com/bandizip](https://www.bandisoft.com/bandizip))

Вот, что я изменил в своем файле [config.plist](/EFI/CLOVER/config.plist):

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
                  <dict>
					<key>Comment</key>
					<string>change _OSI to XOSI</string>
					<key>Disabled</key>
					<false/>
					<key>Find</key>
					<data>
					X09TSQ==
					</data>
					<key>Replace</key>
					<data>
					WE9TSQ==
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
                <key>PluginType</key>
								<string>1</string>
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

Это не рабочий config.plist. Выше я привел только те пункты, которые были изменены по сравнению с родным конфигом из ISO образа Clover ревизии 5033.

Такой SMBIOS подойдет для загрузки, но потом лучше сгенерировать его пункты полностью, например с помощью Clover Configurator.

Так же вам не помешает прочитать книгу "[Clover цвета хаки](https://sourceforge.net/projects/cloverefiboot/files/Documents/)", чтобы понимать какие пункты в config.plist за что отвечают.

#### Пояснения

---

Аргумент загрузки `uia_exclude=HS07` используется вместе с кекстом [USBInjectAll](/docs/RUS/Configuring/InstalledKexts.md). Я использовал эту "связку", чтобы отключить Bluetooth в хакинтоше.

Что писать вам вместо `HS07` вы можете узнать с помощью [IORegistryExplorer](/docs/RUS/ProgramsList/HackintoshTools.md), задав  поиск по слову "bluetooth".

Мне понадобилось отключить Bluetooth при дополнительном обновлении macOS Mojave 10.14.6, потому что обновление [не хотело устанавливаться](https://vk.com/wall-12954845_488300) из-за каких-то проблем с Bluetooth. Так же отключенный модуль не будет тратить энергию аккумулятора, что даст небольшой прирост к автономности.

---