# keyboardの設定ことはじめ

#### レイアウト
* KLEでレイアウトを決める


#### firmware with keyboard firmware builder
* kle.jsonを https://kbfirmware.com/ にロードして、keymapをきめる

### firmware with qmk

see [docker start guide](https://docs.qmk.fm/#/getting_started_docker?id=docker-quick-start)

git clone
```
# original
git clone --recurse-submodules https://github.com/yohabe/qmk_firmware.git
cd qmk_firmware
```

```
# ble micropro
git clone --depth 1 -b dev/ble_micro_pro https://github.com/sekigon-gonnoc/qmk_firmware.git qmk_firmware_bmp
cd qmk_firmware_bmp
```

```
docker run --rm -it  \
	--user root \
	-w /qmk_firmware_bmp \
	-v .:/qmk_firmware_bmp \
	-e ALT_GET_KEYBOARDS=true \
	-e SKIP_GIT="$SKIP_GIT" \
	-e MAKEFLAGS="$MAKEFLAGS" \
	qmkfm/base_container \
  /bin/sh
```



新しいキーボードを定義
```
docker$ util/new_keyboard.sh
Generating a new QMK keyboard directory

Keyboard Name: abc
Keyboard Type [avr]:
Your Name: abcd

Copying base template files... done
Copying avr template files... done
Renaming keyboard files... done
Replacing %YEAR% with 2020... done
Replacing %KEYBOARD% with abc... done
Replacing %YOUR_NAME% with abcd... done

Created a new keyboard called abc.

To start working on things, cd into keyboards/abc,
or open the directory in your favourite text editor.
```

ビルドする
```
make yohabe_su120:default
```


#### ロード
qmk toolboxでpro microにロード

# su120 13x4
* keyboard layout editorの設定 http://www.keyboard-layout-editor.com/#/gists/b3c80e7ce552fb34b86d289779264fac
* keyboard firmware builderの設定 [su120_4x13_kfb.json](./su120_4x13_kfb.json)
* [ble qmk configurator](https://sekigon-gonnoc.github.io/qmk_configurator/)のkeymap設定 [ble_qmk_config_keymap.json](./ble_qmk_config_keymap.json)

|rows|pin|
|--|--|
|0|F6|
|1|F7|
|2|B1|
|3|D2|

|cols|pin|
|--|--|
|0|D1|
|1|D0|
|2|D4|
|3|F4|
|4|F5|
|5|B3|
|6|B2|
|7|B6|
|8|C6|
|9|D7|
|10|E6|
|11|B4|
|12|B5|


# gherkin
[頑張ってGherkin 30 key Keyboardを作るぞ！【ファームウェア書き込み編】](https://romly.com/archives/2017/11/gherkin_firmware.html)

[gherkin_kle.json](./gherkin_kle.json)




