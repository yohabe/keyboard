# keyboardの設定

#### 1. レイアウト
* [keyboard layout editor](http://www.keyboard-layout-editor.com/)でレイアウトを決める


#### 2a. firmware with keyboard firmware builder
* kle.jsonを https://kbfirmware.com/ にロードして、keymapをきめる

### 2b. firmware with qmk

see [docker start guide](https://docs.qmk.fm/#/getting_started_docker?id=docker-quick-start)

qmk firmwareを git clone
```
# original
git clone --recurse-submodules https://github.com/yohabe/qmk_firmware.git
cd qmk_firmware
```

ble micropro版のqmk firmwareはこちら
```
# ble micropro
git clone --depth 1 -b dev/ble_micro_pro https://github.com/sekigon-gonnoc/qmk_firmware.git qmk_firmware_bmp
cd qmk_firmware_bmp
```

dockerを起動
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



docker内で、新しいキーボードを定義
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

生成されるファイル

* config.h
```
#define MATRIX_ROW_PINS { F6, F7, B1, D2 }
#define MATRIX_COL_PINS { D1,D0,D4,F4,F5,B3,B2,B6,C6,D7,E6,B4,B5 }
```

* <keyboard_name>.h
```
#define LAYOUT( \
    k00, k01, k02,k03,k04,k05,k06,k07,k08,k09,k010,k011,k012, \
    k10, k11, k12,k13,k14,k15,k16,k17,k18,k19,k110,k111,k112, \
    k20, k21, k22,k23,k24,k25,k26,k27,k28,k29,k210,k211,k212, \
    k30, k31, k32,k33,k34,k35,k36,k37,k38,k39,k310,k311,k312\
) { \
    { k00, k01, k02,k03,k04,k05,k06,k07,k08,k09,k010,k011,k012}, \
    {k10, k11, k12,k13,k14,k15,k16,k17,k18,k19,k110,k111,k112}, \
    {k20, k21, k22,k23,k24,k25,k26,k27,k28,k29,k210,k211,k212}, \
    {k30, k31, k32,k33,k34,k35,k36,k37,k38,k39,k310,k311,k312}, \
}
```

* keymaps/default/keymap.c
```
const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
...
}

```

ビルドする. カレントディレクトリに.hexができる
```
make yohabe_su120:default
```


#### 3. ロード
qmk toolboxでpro microにロード

# su120 13x4
* keyboard layout editorの設定 http://www.keyboard-layout-editor.com/#/gists/b3c80e7ce552fb34b86d289779264fac
* keyboard firmware builderの設定 [su120_4x13_kfb.json](./su120_4x13_kfb.json)
* [ble qmk configurator](https://sekigon-gonnoc.github.io/qmk_configurator/)のkeymap設定 [ble_qmk_config_keymap.json](./ble_qmk_config_keymap.json)

ble qmk configuratorで設定をロードする方法
1. charlesでhttps://api.qmk.fm/v1/keyboards/su120 をフックして [ble_qmk_config_layout.json](./ble_qmk_config_layout.json) を返す。access-control-allow-origin: https://sekigon-gonnoc.github.io をつける
2. charlesでhttps://api.qmk.fm/v1/keyboards/su120/readme をフックして [ble_qmk_config_layout.json](./ble_qmk_config_layout.json)  を返す。access-control-allow-origin: https://sekigon-gonnoc.github.io をつける
3. keymap設定 [ble_qmk_config_keymap.json](./ble_qmk_config_keymap.json)をインポートする

Tools -> Map Local
![image](https://user-images.githubusercontent.com/1799947/111030428-8db52180-8445-11eb-975a-6b4e530cd306.png)

Tools -> Rewrite
![image](https://user-images.githubusercontent.com/1799947/111030516-fdc3a780-8445-11eb-95f7-daebb36f2c4b.png)




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


# nomu30 keymap




