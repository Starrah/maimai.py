# 数据模型

## SongDifficulty 数据类

### 属性

| 字段             | 类型                 | 说明                     |
|------------------|----------------------|------------------------|
| `type`          | `SongType`           | 谱面类型 |
| `difficulty`    | `LevelIndex`         | 难度索引    |
| `level`         | `str`                | 难度标级，如 `14+` |
| `level_value`   | `float`              | 谱面定数           |
| `note_designer` | `str`                | 谱师           |
| `version`       | `int`                | 谱面首次出现版本         |
| `tap_num`       | `int`                | TAP 物量           |
| `hold_num`      | `int`                | HOLD 物量          |
| `slide_num`     | `int`                | SLIDE 物量         |
| `touch_num`     | `int`                | TOUCH 物量         |
| `break_num`     | `int`                | BREAK 物量         |

## SongDifficultyUtage 数据类

### 属性

| 字段          | 类型   | 说明                    |
| ------------- | ------ | ----------------------- |
| `kanji`       | `str`  | 宴铺前缀，如 `协`，`狂` |
| `description` | `str`  | 宴谱描述                |
| `is_buddy`    | `bool` | 是否为 BUDDY (双人) 谱面 |
| `tap_num`     | `int`  | TAP 物量                |
| `hold_num`    | `int`  | HOLD 物量               |
| `slide_num`   | `int`  | SLIDE 物量              |
| `touch_num`   | `int`  | TOUCH 物量              |
| `break_num`   | `int`  | BREAK 物量              |

## SongDifficulties 数据类

### 属性

| 字段         | 类型                     | 说明                     |
|-------------|--------------------------|------------------------|
| `standard`   | `list[SongDifficulty]`    | 标谱难度列表 |
| `dx`        | `list[SongDifficulty]`    | DX谱难度列表       |
| `utage`     | `list[SongDifficultyUtage]`| 宴谱难度列表       |

## Song 数据类

### 属性

| 字段             | 类型                 | 说明                     |
|------------------|----------------------|------------------------|
| `id`             | `int`                | 曲目 ID            |
| `title`          | `str`                | 曲名             |
| `artist`         | `str`                | 艺术家              |
| `genre`          | `str`                | 流派                  |
| `bpm`            | `int`                | 曲目 BPM     |
| `map`            | `str \| None`         | 曲目所属区域     |
| `version`        | `int`                | 曲目首次出现版本         |
| `rights`         | `str \| None`         | 曲目版权信息         |
| `aliases`        | `list[str] \| None`   | 曲目别名列表               |
| `disabled`       | `bool`               | 是否被禁用               |
| `difficulties`   | `SongDifficulties`    | 谱面难度          |

### 方法

```python
def get_levels(self, exclude_remaster: bool = False) -> list[LevelIndex]:
    """获取歌曲的所有难度索引。

    参数:
        exclude_remaster: 是否排除 ReMASTER 等级索引。
    返回:
        歌曲包含的难度索引列表。
    """

def get_diff(self, type: SongType, level_index: LevelIndex) -> SongDifficulty | None:
    """通过谱面类型和难度索引获取歌曲的难度。

    参数:
        type: 谱面类型，例如 `SongType.DX`。
        level_index: 难度索引，例如 `LevelIndex.MASTER`。
    返回:
        歌曲的某个难度，如果不存在则返回 None。
    """
```

## PlayerIdentifier 数据类

### 属性

| 字段             | 类型                     | 说明                     |
|------------------|--------------------------|------------------------|
| `qq`             | `int \| None`             | QQ号                   |
| `username`       | `str \| None`             | 用户名                 |
| `friend_code`    | `int \| None`             | 好友码                 |
| `credentials`    | `str \| Cookies \| None` | 玩家凭据                 |

### 方法

## PlayerTrophy 数据类

### 属性

| 字段     | 类型             | 说明                     |
|-----------------|------------------|------------------------|
| `id`         | `int`           | 称号ID               |
| `name`       | `str`           | 称号名称             |
| `color`      | `str`           | 称号颜色           |

## PlayerIcon 数据类

### 属性

| 字段     | 类型             | 说明                     |
|-----------------|------------------|------------------------|
| `id`         | `int`           | 头像ID               |
| `name`       | `str`           | 头像名称             |
| `genre`      | `str`           | 头像分类     |

## PlayerNamePlate 数据类

### 属性

| 字段     | 类型             | 说明                     |
|-----------------|------------------|------------------------|
| `id`         | `int`           | 姓名框ID              |
| `name`       | `str`           | 姓名框名称            |

## PlayerFrame 数据类

### 属性

| 字段     | 类型             | 说明                     |
|-----------------|------------------|------------------------|
| `id`         | `int`           | 背景ID               |
| `name`       | `str`           | 背景名称            |

## Player 数据类

### 属性

| 字段     | 类型             | 说明                     |
|-----------------|------------------|------------------------|
| `name`       | `str`           | 玩家名称               |
| `rating`     | `int`           | 玩家Rating          |

## DivingFishPlayer 数据类

继承自 `Player` 类。

### 属性

| 字段           | 类型             | 说明                     |
|----------------|------------------|------------------------|
| `nickname`     | `str`           | 玩家昵称            |
| `plate`        | `str`           | 玩家牌子          |
| `additional_rating` | `int` |  |

## LXNSPlayer 数据类

继承自 `Player` 类。

### 属性

| 字段             | 类型                     | 说明                     |
|------------------|--------------------------|------------------------|
| `friend_code`    | `int`                    | 玩家好友码             |
| `trophy`        | `PlayerTrophy`           | 玩家称号             |
| `course_rank`    | `int`                    | 段位 ID    |
| `class_rank`     | `int`                    | 阶级 ID      |
| `star`           | `int`                    | 搭档觉醒数          |
| `icon`          | `PlayerIcon \| None`       | 头像             |
| `name_plate`     | `PlayerNamePlate \| None` | 姓名框           |
| `frame`          | `PlayerFrame \| None`     | 背景            |
| `upload_time`    | `str`                   | 玩家被同步时的 UTC 时间 |

## SongAlias 数据类

### 属性

| 字段           | 类型             | 说明                     |
|----------------|------------------|------------------------|
| `song_id`      | `int`           | 曲目ID            |
| `aliases`      | `list[str]`      | 曲目别名列表               |

## Score 数据类

### 属性

| 字段           | 类型           | 说明            |
| -------------- | -------------- | --------------- |
| `id`           | `int`          | 曲目ID              |
| `song_name`    | `str`          | 曲名            |
| `level`        | `str`          | 难度标级，如 `14+` |
| `level_index`  | `LevelIndex`   | 难度索引      |
| `achievements` | `float \| None` | 达成率          |
| `fc`           | `FCType`       | FULL COMBO 类型 |
| `fs`           | `FSType`       | FULL SYNC 类型  |
| `dx_score`     | `int \| None`   | DX分数          |
| `dx_rating`    | `float \| None` | DX Rating       |
| `rate`         | `RateType`     | 评级类型   |
| `type`         | `SongType`     | 谱面类型      |

### 方法

```python
def compare(self, other: "Score") -> "Score":
    """比较两个分数，返回更好的分数。"""
```

## PlateObject 数据类

### 属性

| 字段     | 类型                     | 说明                     |
|-----------------|------------------|------------------------|
| `song`       | `Song`           | 歌曲               |
| `levels`      | `list[LevelIndex]` | 难度索引列表           |
| `score`       | `list[Score] \| None` | 成绩列表             |

