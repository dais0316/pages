# Macの初期設定

参考サイト
* [Mac を買ったら必ずやっておきたい初期設定 \- Qiita](https://qiita.com/ucan-lab/items/c1a12c20c878d6fb1e21)

# 最初にやること

* ソフトウェア・アップデート
* 「システム環境設定」から
  * 「Dock」、「最近使ったアプリケーションをDockに表示」をチェックオフ
  * 「Bluetooth」、「Bluetoothをオフにする」
  * 「キーボード」、「キーボード」タブから「修飾キー」、「Caps Lock」キーを「Control」にする
  * 「日付と時刻」、「時計」タブから、「日付を表示」にする。
  * 「共有」、「コンピュータ名」をシンプルな名前にする(e.g.: MacbookAir)
  * 「Spotlight」、「検索結果」より必要なものだけに絞る
    * Spotlightの検索候補、アプリケーション、フォルダ、計算機

# Finder

「環境設定」から、

* 「一般」タブから、「ハードディスク」にチェックする。「新規Finderウィンドウで次を表示」するから、ホームディレクトリにする
* 「サイドバー」タブから、「最近の項目」と「AirDrop」と「タグ」のチェックを外し、「ホームディレクトリ」にチェック、

## LanDiskに接続する

* [MacOS X 10.9 で少し古い LinkStation に AFP で接続する方法](https://align-centre.hatenablog.com/entry/2014/06/10/134954)

```shell
ls com.apple.Apple* # com.apple.AppleShareClient.plistが無いことを確認する
sudo defaults write /Library/Preferences/com.apple.AppleShareClient afp_disabled_uams -array "Cleartxt Passwrd" "MS2.0" "2-Way Randnum exchange"
defaults read /Library/Preferences/com.apple.AppleShareClient afp_disabled_uams
```

次が表示されたらOK

```
(
    "Cleartxt Passwrd",
    "MS2.0",
    "2-Way Randnum  exchange"
)
```

今後は、Windows Storage Server を搭載した NAS がベスト、のようだ。

他にも。

* [MavericksにしたらNASがおかしい、そんなときの対策](https://news.mynavi.jp/article/osxhack-110/)

# 仮想ディスプレイ

* 「Ctrl + ↑」でMission Controlが開いたら、右上にある「+」で「デスクトップ X」を追加する

# ターミナル設定

* 「環境設定」から
  * プロファイルは、Proをベースに複製する
  * テキストはアンチエイリアス処理をチェックする
  * フォントはMonaco 10pt

## シェル設定

* bashに切り替え

```shell
$ chsh -s /bin/bash
```

「デフォルトのシェルはzshにしろ」とメッセージが出るが、これを消すには「~/.bash_profile」に追記する。

```shell
$ echo "export BASH_SILENCE_DEPRECATION_WARNING=1" >> ~/.bash_profile
```

## 隠しファイルを表示する

```shell
$ defaults write com.apple.finder AppleShowAllFiles -boolean true
```

## 共有フォルダで.DS_Storeを作成しない

```shell
$ defaults write com.apple.desktopservices DSDontWriteNetworkStores true
```

## Homebrew

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

brew update
brew cask upgrade

brew cask install 4k-video-downloader
brew cask install appcleaner # SmartDeleteをOnにする
brew cask install biscuit
brew cask install cakebrew
brew cask install ccleaner
brew cask install coteditor
brew cask install firealpaca
brew cask install firefox
#brew tap caskroom/fonts
brew cask install freemind
brew cask install google-chrome
#brew cask install google-japanese-ime # しばらく「ことえり」を使ってみよう。
brew cask install iina
brew cask install iterm2
brew cask install lastpass
brew cask install macwinzipper
brew cask install messenger
brew cask install monolingual #"Language"から、日本語と英語以外を選択、"Archtecture"から、Intel-64-bitのもの以外を選択し、削除する（それぞれ７９９．３MBと23.8MBの節約）。
brew cask install namechanger
brew cask install onyx
brew cask install rectangle
brew cask install r
brew cask install rstudio
brew cask install seashore
brew cask install simple-comic
brew cask install skitch
brew cask install spotify
brew cask install typora
brew cask install whatsapp
brew cask install the-unarchiver
brew cask install visual-studio-code

#brew cask install cd-to-iterm

brew cask upgrade

brew install mackup
#brew install octave

brew install pyenv
brew install pyenv-virtualenv

brew cleanup
#brew cask cleanup
brew doctor
```

## starship

* https://starship.rs
* [iTerm2とstarshipでterminalとshellをお洒落にしました！ \- Qiita](https://qiita.com/macololidoll/items/1c369217c6203dd479bd)

```shell
brew install starship
echo 'eval "$(starship init bash)"' >> ~/.bash_profile
exec $SHELL -l
 ```
 
 ### starship設定ファイル
 
 ```shell
 mkdir ~/.config
 touch ~/.config/starship.toml
 ```
 
 ```
 # Disable the newline at the start of the prompt
add_newline = false

[character]
symbol = "➜"
error_symbol = "✗"
use_symbol_for_status = true

[directory]
truncate_to_repo = false

[git_branch]
symbol = "🌱 "
truncation_length = 4
truncation_symbol = ""

[time]
disabled = false
format = "🕙[ %T ]"
utc_time_offset = "+9"
 ```
 
# Google Add-on

* [ato-ichinen](https://chrome.google.com/webstore/detail/ato-ichinen/pojaolkbbklmcifckclknpolncdmbaph?hl=ja)
* [AutoPagerize](https://chrome.google.com/webstore/detail/autopagerize/igiofjhpmpihnifddepnpngfjhkfenbp?hl=ja)
* [Adblocker for YouTube](https://chrome.google.com/webstore/detail/adblocker-for-youtube/ldkihpcibakajmpnggbjnehoifnnpebn?hl=ja)
* [Back to Back](https://chrome.google.com/webstore/detail/back-to-back/jegdggknidpkiahafcbphabbjcahildm?hl=ja)
* [Create Link](https://chrome.google.com/webstore/detail/create-link/gcmghdmnkfdbncmnmlkkglmnnhagajbm?hl=ja)
* Flash Video Downloader
* [HTTPS Everywhere](https://chrome.google.com/webstore/detail/https-everywhere/gcbommkclmclpchllfjekcdonpmejbdp?hl=ja)
* [Keepa - Amazon Price Tracker](https://chrome.google.com/webstore/detail/keepa-amazon-price-tracke/neebplgakaahbhdphmkckjjcegoiijjo?hl=ja)
* [LastPass: Free Password Manager](https://chrome.google.com/webstore/detail/lastpass-free-password-ma/hdokiejnpimakedhajhdlcegeplioahd?hl=ja)
* [OneClick Cleaner for Chrome](https://chrome.google.com/webstore/detail/oneclick-cleaner-for-chro/oncckmaelaecccmaniihojgeopkcajfh?hl=ja)_
* [OneTab](https://chrome.google.com/webstore/detail/onetab/chphlpgkkbolifaimnlloiipkdnihall?hl=ja)
* [Peek-a-tab](https://chrome.google.com/webstore/detail/peek-a-tab-tabs-manager-f/nnpdamdaknpnohmlbnmgphiodghbohop?hl=ja)
* [PrintWhatYouLike](https://chrome.google.com/webstore/detail/printwhatyoulike/npgfabafajliaooeicdoahbpoajfmbbe?hl=ja)
* [Save to Pocket](https://chrome.google.com/webstore/detail/save-to-pocket/niloccemoadcdkdjlinkgdfekeahmflj?hl=ja)
* [Simplify Gmail](https://chrome.google.com/webstore/detail/simplify-gmail/pbmlfaiicoikhdbjagjbglnbfcbcojpj?hl=ja)
* [Tampermonkey](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=ja)
* Vue.js devtools
* Wappalyzer
* [その本、図書館にあります。](https://chrome.google.com/webstore/detail/その本、図書館にあります%E3%80%82/ldidobiipljjgfaglokcehmiljadanle?hl=ja)
* [アマゾン注文履歴フィルタ](https://chrome.google.com/webstore/detail/その本、図書館にあります%E3%80%82/ldidobiipljjgfaglokcehmiljadanle?hl=ja)
* ストリームレコーダー
* [自動価格比較／ショッピング検索（Auto Price Checker）](https://chrome.google.com/webstore/detail/自動価格比較%EF%BC%8Fショッピング検索（auto-pric/hafkflejlikjnadiclapppceddoielio?hl=ja)

# Firefox

* Download Star
* Keepa - Amazon Price Tracker
* LastPass: Free Password Manager
* Sea Containers
* Simplify Gmail
* Tampermonkey
* Tile Pages WE

# Visual Studio Code

* [【初心者】VSCodeの設定同期エクステンション「Setting Sync」](https://qiita.com/tomokei5634/items/22128efe306ce9bc5682)
  * [Settings Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync)

* Auto Close Tag
* Auto Rename Tag
* Auto-Open Markdown Preview
* Better Comment
* Better Comments
* Bracket Pair Colorizer 2
* Code Blue
* DotENV
* Dracula Theme
* Evillnspector
* Git History
* indent-rainbow
* Japanese Language Pack for VSC
* Markdown All in One
* Markdown PDF
* Markdown Preview Enhanced
* Markdown TOC
* Markdown+Math
* Material Icon Theme
* Output Colorizer
* PlantUML
* Poor Man's T-SQL Formatter
* Pretttier - Code formatter
* Pyright
* Python
* Rainbow CSV
* Regex Previewer
* Remote - Containers
* Remote - SSH
* Remote - SSH: Editing Configuration Files
* Remote - SSH: Explorer
* Remote - WSL
* Remote Development
* Setting Sync
* Spell Right
* SQLTools - Database tools
* Trailing Spaces
* Vetur
* Visual Studio IntelliCode
* vscode-icons
* テキスト構成くん
 
