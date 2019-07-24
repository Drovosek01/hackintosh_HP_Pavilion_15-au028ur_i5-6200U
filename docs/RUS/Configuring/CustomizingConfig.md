### Настройка файла config.plist

Здесь описано то, как я изменил чистый конфиг, который идет вместе с Clover ревизии 5018.

Вы можете скачать образ диска с данным конфигом с официальной страницы загрузчика Clover: https://sourceforge.net/projects/cloverefiboot/files/Bootable_ISO/ Для распаковки .lzma и .tar файлов в Windows лучше используйте [7zip](https://www.7-zip.org/) или [Bandizip]([https://bandisoft.com/bandizip](https://www.bandisoft.com/bandizip))

Вот, что я изменил в своем файле config.plist:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>ACPI</key>
	<dict>
		<key>DSDT</key>
		<dict>
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
			</array>
		</dict>
	</dict>
	<key>Boot</key>
	<dict>
		<key>Arguments</key>
		<string>-wegnoegpu darkwake=0</string>
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
</dict>
</plist>
```

Это не рабочий config.plist. Выше я привел только те пункты, которые были изменены по сравнению с родным конфигом из ISO образа Clover ревизии 4972.

Такой SMBIOS подойдет для загрузки, но потом лучше сгенерировать его пункты полностью, например с помощью Clover Configurator.

Так же вам не помешает прочитать книгу "[Clover цвета хаки](https://sourceforge.net/projects/cloverefiboot/files/Documents/)", чтобы понимать какие пункты в config.plist за что отвечают.