# Useful-command-lines

### Terminal Commands

_(text in italic needs to be modified)_

## shortcuts

* 	delete strings

press  **^(control) + W**


## useful commands
	
* 	截图保存路径


```
defaults write com.apple.screencapture location /path/
killall SystemUIServer

```


* 截图文件格式


```
defaults write com.apple.screencapture type jpg
killall SystemUIServer
```


* 	更改 LauchPad 布局

        




```
defaults write com.apple.dock springboard-columns -int ColNum
defaults write com.apple.dock springboard-rows -int RowNum
killall Dock
```





* 	导出 Safari Reading List

        




```
printf '#!/bin/bash\n'"/usr/bin/plutil -convert xml1 -o - ~/Library/Safari/Bookmarks.plist | grep -E -o '<string>http[s]{0,1}://.*</string>' | grep -v icloud | sed -E 's/<\/{0,1}string>//g' | open -f\n" > ExportReadingList.command 
chmod +x ExportReadingList.command 
open -R ExportReadingList.command
```






* 隐藏文件/文件夹

        



```
chflags hidden /Path/
```





* 	显示 App Store 的 Debug 菜单

        




```
defaults write com.apple.appstore ShowDebugMenu -bool true
```






* 	ffmpeg trim video	( -ss for star time, -t for duration time)

        

```
ffmpeg -i <SourceFilePath>  -ss hh:mm:ss -t hh:mm:ss -c copy <OutputFilePath>
```





* 修改文件创建时间(t)/修改时间(mt)
	

```
touch -t [[CC]YY]MMDDhhmm[.SS] [path]
```

* download stream

        

```
ffmpeg -i "https://<domain>/.m3u8" -c:v copy -c:a copy -bsf:a aac_adtstoasc <OutputFilePath>.flv
```


* download Twitter Album (with DownAlbum Extension)

        

```
aria2c --all-proxy=http://127.0.0.1:1087 --remote-time true --log=/Users/username/.aria2/log  -i url.txt
```

    
	
* 	ffmpeg crop then scale video, add chapter to video and encode to h.265 with frame rate 23.976

        

```
ffmpeg -i ExampleInput.mov -i metadata.txt -map_metadata 1  -c:a copy -c:v libx265 -crf 22 -tag:v hvc1 -vf crop=1334:750:0:292,scale=   1280:720 -r 23.976 ExampleOutput.mov
```








* flush DNS cache (source：[flush-dns](https://kinsta.com/jp/knowledgebase/flush-dns/), [Mac の DNS キャッシュ をクリアするコマンド](https://blog.77jp.net/command-to-clear-dns-cache-on-mac), [214981288-Flushing-your-DNS-cache-in-Mac-OS-X-and-Linux](https://help.dreamhost.com/hc/en-us/articles/214981288-Flushing-your-DNS-cache-in-Mac-OS-X-and-Linux))

```
sudo killall -HUP mDNSResponder
```
