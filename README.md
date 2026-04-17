- `holomem.json`: Contains data for holomem cards.
- `oshi.json`: Contains data for Oshi holomem cards.
- `supports.json`: Contains data for Support cards.

**Only JP format text is stored in the files.**

Ability name data may be removed once a localization storage format is designed.
Card name data may be reworked to be a key instead of the full name to include cards with several names (e.g. duos, Aki Rosenthal's Axe)

---

## Data Schema

### `holomem.json`
An array of objects representing holomem cards.

| Field           | Type    | Description                                                                                                                                         |
|:----------------|:--------|:----------------------------------------------------------------------------------------------------------------------------------------------------|
| `Name`          | String  | The name of the holomem.                                                                                                                            |
| `Code`          | String  | The card's code (e.g., `hBP01-009`).                                                                                                                |
| `Color`         | Number  | The color of the card (stored as an **Integer**). See [Color](#color) for values. May be a sum of values if the holomem is a multicolor duo holomem |
| `BloomLevel`    | String  | The bloom level of the card. See [BloomLevel](#bloomlevel) for values.                                                                              |
| `Buzz`          | Boolean | Whether the card is a "Buzz" card.                                                                                                                  |
| `InitialHp`     | Number  | The printed HP of the Holomem.                                                                                                                      |
| `Effects`       | Array   | A list of effects or arts. See [Effect Structure](#effect-structure).                                                                               |
| `BatonPassCost` | Number  | The baton pass cost.                                                                                                                                |

#### Effect Structure
Effects can be of different types. If the type is `Arts`, additional fields are present.

| Field              | Type    | Description                                                                                                               |
|:-------------------|:--------|:--------------------------------------------------------------------------------------------------------------------------|
| `Name`             | String  | The name of the effect/arts.                                                                                              |
| `Type`             | String  | The type of effect. See [HolomemEffectType](#holomemeffecttype) for values.                                               |
| `Damage`           | Integer | (Arts only) The base damage value. Does not include `+` suffix if text can boost this value.                              |
| `TextBoostsDamage` | Boolean | (Arts only) Whether the effect text provides a conditional damage boost.                                                  |
| `UseCost`          | Object  | (Arts only) A dictionary where keys are **Color Strings** and values are Integers representing the cost to use this arts. |
| `CriticalColor`    | Number? | (Arts only) Optional color for critical hits (stored as an Integer).                                                      |
| `CriticalAmount`   | Number? | (Arts only) Optional amount for critical damage. Usually `50` but can be different (see Live Start Deck 2nds)             |

---

### `oshi.json`
An array of objects representing Oshi holomem cards.

| Field    | Type   | Description                                                                                            |
|:---------|:-------|:-------------------------------------------------------------------------------------------------------|
| `Name`   | String | The name of the Oshi holomem member.                                                                   |
| `Code`   | String | The card's code.                                                                                       |
| `Color`  | Number | The color of the card (Integer, may be a sum of values if there's ever a duo Oshi or multicolor Oshi). |
| `Life`   | Number | The printed Life in this Oshi.                                                                         |
| `Skills` | Array  | A list of Oshi skills.                                                                                 |

#### Oshi Skill Structure
| Field  | Type    | Description                                                        |
|:-------|:--------|:-------------------------------------------------------------------|
| `Name` | String  | The name of the skill.                                             |
| `Cost` | Number? | The Holopower cost (null if cost is variable i.e. Lui Oshi Skill). |
| `Type` | String  | The type of skill. See [OshiSkillType](#oshiskilltype).            |

---

### 3. `supports.json`
An array of objects representing various support cards.

| Field     | Type    | Description                                           |
|:----------|:--------|:------------------------------------------------------|
| `Name`    | String  | The name of the card.                                 |
| `Code`    | String  | The card's code.                                      |
| `Type`    | String  | The support subtype. See [SupportType](#supporttype). |
| `Tags`    | Array?  | Optional list of string tags. Null if none            |
| `Limited` | Boolean | Whether the card has a "LIMITED" restriction.         |

---

## Enum Definitions and Storage

All enums marked as **Text** are stored as strings in the JSON files. Enums marked as **Number** are stored as their underlying integer value.

### Color
Stored as: **Number**, **Text** when used as Dictionary Keys.

Values:
- `0`: Neutral
- `1`: White
- `2`: Green
- `4`: Red
- `8`: Blue
- `16`: Purple
- `32`: Yellow

### BloomLevel
Stored as: **Text**

Values:
- `Debut`
- `First`
- `Second`
- `Spot`: Stored as -1 in enum integer values.

### HolomemEffectType
Stored as: **Text**

Values:
- `CollabEffect`
- `BloomEffect`
- `Gift`
- `Arts`

### OshiSkillType
Stored as: **Text**

Values:
- `OshiSkill`
- `SpOshiSkill`
- `OshiStageSkill`: Set 7 onwards.

### SupportType
Stored as: **Text**

Values:
- `Staff`
- `Item`
- `Event`
- `Tool`
- `Mascot`
- `Fan`
