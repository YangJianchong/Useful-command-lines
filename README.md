# Useful-command-lines

<em>(text in italic needs to be modified)</em>

## shortcuts

* delete strings

press `^W`

## useful commands

### System Features
	
* 截图保存路径

<pre><code>defaults write com.apple.screencapture location <em>/path/</em>
killall SystemUIServer</code></pre>

* 截图文件格式

<pre><code>defaults write com.apple.screencapture type <em>jpg</em>
killall SystemUIServer</code></pre>

* 更改 LauchPad 布局

<pre><code>defaults write com.apple.dock springboard-columns -int <em>ColNum</em>
defaults write com.apple.dock springboard-rows -int <em>RowNum</em>
killall Dock</code></pre>

* 导出 Safari Reading List

<pre><code>printf '#!/bin/bash\n'"/usr/bin/plutil -convert xml1 -o - ~/Library/Safari/Bookmarks.plist | grep -E -o '&lt;string&gt;http[s]{0,1}://.*&lt;/string&gt;' | grep -v icloud | sed -E 's/&lt;\/{0,1}string&gt;//g' | open -f\n" > ExportReadingList.command 
chmod +x ExportReadingList.command 
open -R ExportReadingList.command
</code></pre>

* 显示 App Store 的 Debug 菜单

<pre><code>defaults write com.apple.appstore ShowDebugMenu -bool <em>true</em> </code></pre>


* flush DNS cache (source：[flush-dns](https://kinsta.com/jp/knowledgebase/flush-dns/), [Mac の DNS キャッシュ をクリアするコマンド](https://blog.77jp.net/command-to-clear-dns-cache-on-mac), [214981288-Flushing-your-DNS-cache-in-Mac-OS-X-and-Linux](https://help.dreamhost.com/hc/en-us/articles/214981288-Flushing-your-DNS-cache-in-Mac-OS-X-and-Linux))

<pre><code>sudo killall -HUP mDNSResponder</code></pre>

### File Magics

* 隐藏文件/文件夹

<pre><code>chflags hidden <em>/Path/</em></code></pre>

* 修改文件创建时间(`-t`)/修改时间(`mt`)

<pre><code>touch -t <em>[[CC]YY]MMDDhhmm[.ss]</em> <em>/path/</em></code></pre>

* ffmpeg trim video	( -ss for star time, -t for duration time)

### ffmpeg

<pre><code>ffmpeg -i <em>ExampleInput</em> -ss <em>hh:mm:ss</em> -t <em>hh:mm:ss</em> -c copy <em>ExampleOutput.mov</em></code></pre>

* ffmpeg download stream

<pre><code>ffmpeg -i "<em>https://&lt;domain&gt;/.m3u8</em>" -c:v copy -c:a copy -bsf:a aac_adtstoasc <em>ExapmleOutput.flv</em></code></pre>

* ffmpeg crop then scale video, add chapter to video and encode to h.265 with frame rate 23.976

<pre><code>ffmpeg -i <em>ExampleInput.mov</em> -i <em>metadata.txt</em> -map_metadata 1  -c:a copy -c:v libx265 -crf 22 -tag:v hvc1 -vf crop=<em>1334:750:0:292</em>,scale=<em>1280:720</em> -r <em>23.976</em> <em>ExampleOutput.mov</em></code></pre>

### aria2

* download Twitter Album (with DownAlbum Extension)

<pre><code>aria2c --all-proxy=<em>http://address:port</em> --remote-time true --log=<em>/Users/username/.aria2/log</em>  -i <em>url.txt</em></code></pre>
	
