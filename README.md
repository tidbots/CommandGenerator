# RoboCup@home コマンドジェネレータ
オリジナルは　https://github.com/RoboCupAtHome/CommandGenerator
ia
# 使い方
## インストール
venvで動かすので事前にインストールしておいて下さい．
例えば：<br>
Ubuntuの場合
```
$ sudo apt update
$ sudo apt install python3-venv
```

リポジトリのクローン
```
$ cd ~/
$ git clone https://github.com/RoboCupAtHome/CommandGenerator.git
```

競技用のデータのダウンロード
大会テンプレートや過去の大会のデータが[公式リポジトリ](https://github.com/RoboCupAtHome)にあるのでダウンロードして下さい．
- [大会テンプレート](https://github.com/RoboCupAtHome/CompetitionTemplate)
- [Salvador2025](https://github.com/RoboCupAtHome/Salvador2025)
- [Eindhoven2024](https://github.com/RoboCupAtHome/Eindhoven2024)
```
$ cd ~/CommandGenerator
$ git clone https://github.com/RoboCupAtHome/CompetitionTemplate.git

```

```
$ cd ~/CommandGenerator
$ python -m venv venv
$ source venv/bin/activate
$ pip install .
$ athome-generator --help
usage: athome-generator [-h] [-d DATA_DIR] [-p]
Generate Commands for Robocup@Home
options:
  -h, --help            show this help message and exit
  -d DATA_DIR, --data-dir DATA_DIR
                        directory where the data is read from
  -p, --print-config    print parsed data and exit
```


## 実行してみる
```
$ cd ~/CommandGenerator
$ $ athome-generator -d CompetitionTemplate
'1': Any command
'2': Command without manipulation
'3': Command with manipulation
'4': Batch of three commands
'5': Generate EGPSR setup
'0': Generate QR code
'q': Quit"

1
Navigate to the desk lamp then locate the standing person and follow them
2
Escort the sitting person from the tv stand to the trashbin
3
Tell me what is the smallest object on the bookshelf
4
Tell the gesture of the person at the lamp to the person at the desk
Follow Robin from the armchair to the living room
Give me a cup from the bookshelf
```

名前，場所，部屋，オブジェクト，カテゴリーの一覧表示
```
$ athome-generator -d CompetitionTemplate -p
Names:
['Adel', 'Angel', 'Axel', 'Charlie', 'Jane', 'Jules', 'Morgan', 'Paris', 'Robin', 'Simone']
Locations:
['bed', 'bedside table', 'shelf', 'trashbin', 'dishwasher', 'potted plant', 'kitchen table', 'chairs', 'pantry', 'refrigerator', 'sink', 'cabinet', 'coatrack', 'desk', 'armchair', 'desk lamp', 'waste basket', 'tv stand', 'storage rack', 'lamp', 'side tables', 'sofa', 'bookshelf', 'entrance', 'exit']
Locations (p):
['bed', 'bedside table', 'shelf', 'dishwasher', 'kitchen table', 'pantry', 'refrigerator', 'sink', 'cabinet', 'desk', 'tv stand', 'storage rack', 'side tables', 'sofa', 'bookshelf']
Rooms:
['bedroom', 'kitchen', 'office', 'living room', 'bathroom']
Objects:
['juice pack', 'cola', 'milk', 'orange juice', 'tropical juice', 'red wine', 'iced tea', 'tennis ball', 'rubiks cube', 'baseball', 'soccer ball', 'dice', 'orange', 'pear', 'peach', 'strawberry', 'apple', 'lemon', 'banana', 'plum', 'cornflakes', 'pringles', 'cheezit', 'cup', 'bowl', 'fork', 'plate', 'knife', 'spoon', 'chocolate jello', 'coffee grounds', 'mustard', 'tomato soup', 'tuna', 'strawberry jello', 'spam', 'sugar', 'cleanser', 'sponge']
Categories:
[('drink', 'drinks'), ('toy', 'toys'), ('fruit', 'fruits'), ('snack', 'snacks'), ('dish', 'dishes'), ('food', 'food'), ('cleaning supply', 'cleaning supplies')]
```



# Instructions

## Install

With tool of your choice. e.g. venv and pip

- `python -m venv venv`
- 
- `source venv/bin/activate`
- `pip install .`
- `athome-generator --help`

## Commandline Generator

```
usage: athome-generator [-h] [-d DATA_DIR] [-p]

Generate Commands for Robocup@Home

options:
  -h, --help            show this help message and exit
  -d DATA_DIR, --data-dir DATA_DIR
                        directory where the data is read from
  -p, --print-config    print parsed data and exit
```

Run the generator for the given DATA_DIR
- `athome-generator -d DATA_DIR`

For an example layout check out the: [CompetitionTemplate](https://github.com/RoboCupAtHome/CompetitionTemplate)

## GPSR UI

[nicegui](https://nicegui.io/) UI for GPSR generator. Supports rephrasing via openai compatible llm apis over `http://{host}:{port}/v1/chat/completions`. 

```
athome-generator-gpsr-ui --help
usage: athome-generator-gpsr-ui [-h] [-u URL] [--host HOST] [--port PORT] [-a API_KEY] [-d DATA_DIR]

robocupathome GPSR-UI for usage in competitions

options:
  -h, --help            show this help message and exit
  -u URL, --url URL     Full URL to OpenAI compatible Chat API
  --host HOST           LLM host
  --port PORT           LLM port
  -a API_KEY, --api-key API_KEY
                        LLM API Key
  -d DATA_DIR, --data-dir DATA_DIR
                        directory where the data is read from
```

<img src="docs/gpsr-ui-ref.png" alt="Generate View" style="width:45%; height:auto;">
<img src="docs/gpsr-ui.png" alt="Display View" style="width:45%; height:auto;">
