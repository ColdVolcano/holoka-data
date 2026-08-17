- `holomem.json`: Contains data for holomem cards.
- `oshi.json`: Contains data for Oshi holomem cards.
- `supports.json`: Contains data for Support cards.
- `cheers.json`: Contains data for Cheer cards.

**Only JP format text is stored in the files.**

Ability names (Arts, effects, and Oshi skills) are not stored and are expected to be handled by localization. Other text data may be removed once a localization storage format is designed.

---

## Data Schema

Each file is a JSON object whose keys are card codes (e.g., `hBP01-009`), so a card can be looked up directly by its code. The code is not repeated as a field inside the entries.

### `holomem.json`

An object keyed by card code, containing holomem card data.

| Field           | Type    | Description                                                                                                                                         |
| :-------------- | :------ | :-------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Name`          | String  | The name of the holomem.                                                                                                                            |
| `Color`         | Number  | The color of the card (stored as an **Integer**). See [Color](#color) for values. May be a sum of values if the holomem is a multicolor duo holomem |
| `BloomLevel`    | String  | The bloom level of the card. See [BloomLevel](#bloomlevel) for values.                                                                              |
| `Buzz`          | Boolean | Whether the card is a "Buzz" card.                                                                                                                  |
| `InitialHp`     | Number  | The printed HP of the holomem.                                                                                                                      |
| `Effects`       | Array   | A list of effects or arts. See [Effect Structure](#effect-structure).                                                                               |
| `Tags`          | Array   | The list of tags of the holomem.                                                                                                                    |
| `BatonPassCost` | Number  | The baton pass cost.                                                                                                                                |
| `ExtraRule`     | Number? | The Extra Rule types in the holomem. Omitted if the holomem has no Extra Rules.                                                                     |
| `ExtraNames`    | Array?  | The names added to the card by its Extra Rules. Only present when `ExtraRule` includes `8`.                                                         |

#### Effect Structure

Effects can be of different types. If the type is not `Arts`, the effect contains only `Type`. If the type is `Arts`, additional fields are present.

| Field                | Type    | Description                                                                                                                                       |
| :------------------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Type`               | String  | The type of effect. See [HolomemEffectType](#holomemeffecttype) for values.                                                                       |
| `Damage`             | Integer | (Arts only) The base damage value. Does not include `+` suffix if text can boost this value.                                                      |
| `TextBoostBehaviour` | String? | (Arts only) Present when the effect text can boost the damage value. The only current value is `Boost` (the damage is printed with a `+` suffix). |
| `UseCost`            | Object  | (Arts only) A dictionary where keys are **Color Strings** and values are Integers representing the cost to use this arts.                         |
| `CriticalColor`      | Number? | (Arts only) Optional color for critical hits (stored as an Integer). Null if the Arts has no critical.                                            |
| `CriticalAmount`     | Number? | (Arts only) Optional amount for critical damage. Usually `50` but can be different (see Live Start Deck 2nds). Null if the Arts has no critical.  |

---

### `oshi.json`

An object keyed by card code, containing Oshi holomem card data.

| Field    | Type   | Description                                                                                            |
| :------- | :----- | :----------------------------------------------------------------------------------------------------- |
| `Name`   | String | The name of the Oshi holomem member.                                                                   |
| `Color`  | Number | The color of the card (Integer, may be a sum of values if there's ever a duo Oshi or multicolor Oshi). |
| `Life`   | Number | The printed Life in this Oshi.                                                                         |
| `Skills` | Array  | A list of Oshi skills.                                                                                 |

#### Oshi Skill Structure

| Field  | Type    | Description                                                        |
| :----- | :------ | :----------------------------------------------------------------- |
| `Cost` | Number? | The Holopower cost (null if cost is variable i.e. Lui Oshi Skill). |
| `Type` | String  | The type of skill. See [OshiSkillType](#oshiskilltype).            |

---

### `supports.json`

An object keyed by card code, containing various support card data.

| Field        | Type    | Description                                                                                 |
| :----------- | :------ | :------------------------------------------------------------------------------------------ |
| `Name`       | String  | The name of the card.                                                                       |
| `Type`       | String  | The support subtype. See [SupportType](#supporttype).                                       |
| `Tags`       | Array?  | Optional list of string tags.                                                               |
| `Limited`    | Boolean | Whether the card has a "LIMITED" restriction.                                               |
| `ExtraRule`  | Number? | The Extra Rule types in the card. Omitted if the card has no Extra Rules.                   |
| `ExtraNames` | Array?  | The names added to the card by its Extra Rules. Only present when `ExtraRule` includes `8`. |

---

### `cheers.json`

An object keyed by card code, containing Cheer card data.

| Field   | Type   | Description                                                                       |
| :------ | :----- | :-------------------------------------------------------------------------------- |
| `Name`  | String | The name of the Cheer card.                                                       |
| `Color` | Number | The color of the card (stored as an **Integer**). See [Color](#color) for values. |

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

### ExtraType

Stored as: **Number**

Values:

- `1`: "You may include any number of this holomem in the deck"
- `2`: "This holomem cannot Bloom"
- `4`: "If this holomem is downed, you get Life-2"
- `8`: "This card is also regarded as one or more extra names"
