# Translate current selected text in Ms Word or any other input box by using AppleScript. 
# 通过使用AppleScript翻译Word或任何其他输入框中的当前选定文本。 

## Here's the code:

```
tell application "System Events"
	keystroke "c" using {command down}
	delay 0.05
end tell

set authKey to "your deepl API"
set targetLang to "ZH"

set sourceText to the clipboard
set curlCmd to "curl -X POST 'https://api-free.deepl.com/v2/translate' -H 'Authorization: DeepL-Auth-Key " & authKey & "' -d 'text=" & sourceText & "' -d 'target_lang=" & targetLang & "'"

set jsonResponse to do shell script curlCmd

set textStartMarker to "\"text\":\""
set textEndMarker to "\"}"

set textStartIndex to (offset of textStartMarker in jsonResponse) + (length of textStartMarker)
set textEndIndex to (offset of textEndMarker in jsonResponse) - 1

set translatedText to text textStartIndex thru textEndIndex of jsonResponse

set the clipboard to translatedText

tell application "System Events"
	delay 0.05
	keystroke "v" using {command down}
end tell
```

## steps:
1. install BetterTouchTool 安装 BetterTouchTool 
2. add a short cut trigger  增加一个捷径触发器 
<img width="1106" alt="Screen Shot 2023-03-28 at 10 06 54 AM" src="https://user-images.githubusercontent.com/52094557/228108701-98ff64a3-3ed2-43ef-80f4-4a38fd7cd65e.png">

3. choose AppleScript, copy and paste the code above. 选择AppleScript，复制并粘贴上面的代码。
<img width="1201" alt="Screen Shot 2023-03-28 at 10 07 15 AM" src="https://user-images.githubusercontent.com/52094557/228108721-8d3252e0-91f8-4a98-9c73-cd8a5ea96dbc.png">
<img width="1098" alt="Screen Shot 2023-03-28 at 10 07 29 AM" src="https://user-images.githubusercontent.com/52094557/228108743-9cb8a2f1-89ac-457d-a821-db5892e21fec.png">


## Demo:

![2023-03-28 10 16 20](https://user-images.githubusercontent.com/52094557/228109924-47731fd4-3eaf-4ec8-b570-0bbebe1541f7.gif)

![2023-03-28 10 12 31](https://user-images.githubusercontent.com/52094557/228110288-542e761c-ca53-4672-9cd5-ae663ce1321f.gif)


