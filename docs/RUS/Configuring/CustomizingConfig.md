### Настройка файла config.plist

Здесь описано то, как я изменил чистый конфиг, который идет вместе с Clover ревизии 5033.

Вы можете скачать образ диска с данным конфигом с официальной страницы загрузчика Clover: https://sourceforge.net/projects/cloverefiboot/files/Bootable_ISO/ Для распаковки .lzma и .tar файлов в Windows лучше используйте [7zip](https://www.7-zip.org/) или [Bandizip]([https://bandisoft.com/bandizip](https://www.bandisoft.com/bandizip))

Вот, что я добавил в своем файле [config.plist](/EFI/CLOVER/config.plist), по сравнению со стандартным конфигом, который идет в [ISO](https://github.com/CloverHackyColor/CloverBootloader/releases) образе загрузчика:

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
			<key>Name</key>
			<string>DSDT.aml</string>
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
		<key>DropTables</key>
		<array>
			<dict>
				<key>Signature</key>
				<string>DMAR</string>
			</dict>
		</array>
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
		<key>Audio</key>
		<dict>
			<key>Inject</key>
			<integer>13</integer>
		</dict>
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
		<key>PlayAsync</key>
		<true/>
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
		<key>AppleIntelCPUPM</key>
		<false/>
		<key>KernelPm</key>
		<true/>
	</dict>
	<key>RtVariables</key>
	<dict>
		<key>CsrActiveConfig</key>
		<string>0x67</string>
		<key>MLB</key>
		<string>C02630130GUHMHKAD</string>
	</dict>
	<key>SMBIOS</key>
	<dict>
		<key>BiosReleaseDate</key>
		<string>05/25/2019</string>
		<key>BiosVendor</key>
		<string>Apple Inc.</string>
		<key>BiosVersion</key>
		<string>MBP131.88Z.F000.B00.1905251430</string>
		<key>Board-ID</key>
		<string>Mac-473D31EABEB93F9B</string>
		<key>BoardManufacturer</key>
		<string>Apple Inc.</string>
		<key>BoardSerialNumber</key>
		<string>C02743270QXHMHK1M</string>
		<key>BoardType</key>
		<integer>10</integer>
		<key>BoardVersion</key>
		<string>1.0</string>
		<key>ChassisAssetTag</key>
		<string>MacBook-Aluminum</string>
		<key>ChassisManufacturer</key>
		<string>Apple Inc.</string>
		<key>ChassisType</key>
		<string>0x09</string>
		<key>EfiVersion</key>
		<string>234.0.0.0.0</string>
		<key>Family</key>
		<string>MacBook Pro</string>
		<key>FirmwareFeatures</key>
		<string>0xFC0FE137</string>
		<key>FirmwareFeaturesMask</key>
		<string>0xFF1FFF3F</string>
		<key>LocationInChassis</key>
		<string>Part Component</string>
		<key>Manufacturer</key>
		<string>Apple Inc.</string>
		<key>Mobile</key>
		<true/>
		<key>PlatformFeature</key>
		<string>0x1A</string>
		<key>ProductName</key>
		<string>MacBookPro13,1</string>
		<key>SerialNumber</key>
		<string>C02VL0YMGVC1</string>
		<key>SmUUID</key>
		<string>189518EF-D1DD-4B32-A197-78E35BE4D1D0</string>
		<key>Version</key>
		<string>1.0</string>
	</dict>
	<key>SystemParameters</key>
	<dict>
		<key>InjectKexts</key>
		<string>Yes</string>
	</dict>
</dict>
</plist>
```

Это не рабочий config.plist. Выше я привел только те пункты, которые я добавил в стандартный конфиг, из [ISO](https://github.com/CloverHackyColor/CloverBootloader/releases) образа Clover ревизии 5096, но есть и пункты, которые были удалены из стандартного конфига и я не могу отобразить это каким-то правильным образом в `xml` коде. Если вы просто хотите установить хакинтош, то просто возьмите мой готовый конфиг из этого репозитория из [/EFI/CLOVER/config.plist](/EFI/CLOVER/config.plist), а если вы хотите разобраться в разнице стандартного конфига и того, который используется в этой хакинтош сборке, то вам для начала нужно прочитать книгу "[Clover цвета хаки](https://sourceforge.net/projects/cloverefiboot/files/Documents/)", чтобы понимать какие пункты в config.plist за что отвечают. После этого можно воспользоваться инструментом [diffchecker](https://www.diffchecker.com/) и в нем уже наглядно увидеть что удалено, а чтодобавлено в стандартный конфиг. Так же, чтобы сравнение в diffchecker было более точное, лучше пересохраните ваш/мой конфиг в PlistEditPro (просто откройте файл config.plist этой программой, а потом сохраните) и так же пересохраните стандартный конфиг Clover из ISO образа, а потом уже копируйте код из них. Это нужно потому, что при сохранении PlistEditPro сортирует `xml` файл и я свой config.plist уже сохранил через PlistEditPro, но стандартный config.plist в ISO образе Clover не сохранялся через PlistEditPro и если вы будете так сравнивать свой и стандартный config.plist через diffchecker, то будет найдено много "мусорных" различий, потому что одни и те же строчки могут находится в разных концах файла (образно говоря).

Такой SMBIOS подойдет для загрузки, но потом лучше сгенерировать его пункты полностью, например с помощью Clover Configurator.

Так же вам не помешает прочитать книгу "[Clover цвета хаки](https://sourceforge.net/projects/cloverefiboot/files/Documents/)", чтобы понимать какие пункты в config.plist за что отвечают.

#### Пояснения

---

Аргумент загрузки `uia_exclude=HS07` используется вместе с кекстом [USBInjectAll](/docs/RUS/Configuring/InstalledKexts.md). Я использовал эту "связку", чтобы отключить Bluetooth в хакинтоше.

Что писать вам вместо `HS07` вы можете узнать с помощью [IORegistryExplorer](/docs/RUS/ProgramsList/HackintoshTools.md), задав  поиск по слову "bluetooth".

Мне понадобилось отключить Bluetooth при дополнительном обновлении macOS Mojave 10.14.6, потому что обновление [не хотело устанавливаться](https://vk.com/wall-12954845_488300) из-за каких-то проблем с Bluetooth. Так же отключенный модуль не будет тратить энергию аккумулятора, что даст небольшой прирост к автономности.

---