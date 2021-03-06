## Telefonnummer

[![npm version](https://badge.fury.io/js/telefonnummer.svg)](https://badge.fury.io/js/telefonnummer)
[![Build Status](https://travis-ci.org/believer/telefonnummer.svg?branch=master)](https://travis-ci.org/believer/telefonnummer)
[![Code Climate](https://codeclimate.com/github/believer/telefonnummer/badges/gpa.svg)](https://codeclimate.com/github/believer/telefonnummer)
[![Test Coverage](https://codeclimate.com/github/believer/telefonnummer/badges/coverage.svg)](https://codeclimate.com/github/believer/telefonnummer/coverage)
[![Known Vulnerabilities](https://snyk.io/test/github/believer/telefonnummer/badge.svg)](https://snyk.io/test/github/believer/telefonnummer)

_Telefonnummer_ is phone number in Swedish. This package formats all Swedish phone numbers, both mobile and landline, to a standard format. Area code information is provided by [Post- och telestyrelsen (PTS)](https://www.pts.se/upload/Faktablad/SE/2011/faktablad-riktnummer-nummerordning-pts-f-211_2.pdf).

### Installation

```
npm install telefonnummer --save
```

### Parse

```js
parse(phoneNumber: string, separator?: string): string
```

Take a phone number and return a parsed version of the number. Parser is also default export of package, but might be removed as default in the future.

#### Example

```js
import { parse } from 'telefonnummer'

parse('222') // Röstbrevlåda (Voicemail in Swedish)
parse('0701234567') // 070-123 45 67
parse('468123456') // 08-12 34 56
parse('031626262') // 031-62 62 62
parse('050012345') // 0500-123 45

// With custom separator
parse('0701234567', ':') // 070:123 45 67
```

### Area code

```js
areaCode(area: string): string
```

Returns the area code of the provided city

#### Example

```js
import { areaCode } from 'telefonnummer'

areaCode('Stockholm') // 08
areaCode('Korpilombolo') // 0977
```

### Numbering area

```js
numberingArea(areaCode: string | number): string
```

Returns the numbering area for a provided area code or phone number. Also handles numbers without leading zero.

#### Example

```js
import { numberingArea } from 'telefonnummer'

numberingArea('0977-123 45') // Korpilombolo
numberingArea('081234567') // Stockholm
numberingArea('08') // Stockholm
numberingArea('031') // Göteborg
numberingArea(8) // Stockholm
```

### Validator

```js
validator(phoneNumber: string): boolean
```

Validates both mobile and landline numbers.

#### Example

```js
import { validator } from 'telefonnummer'

validator('0977-123 45') // true
validator('081234567') // true
validator('050012123456') // false
```

### Area codes

```js
areaCodes(): string[]
```

Returns a number sorted array of all the area codes.

#### Example

```js
import { areaCodes } from 'telefonnummer'

areaCodes()
//  [
//    '011 Norrköping',
//    '0120 Åtvidaberg',
//    '0121 Söderköping',
//    ....
//  ]
```

### Normalize

```js
normalize(string): string
```

Clean up any non-digits and country codes from phone number.

#### Example

```js
import { normalize } from 'telefonnummer'

normalize('070-123.45x67') // 0701234567
normalize('+46701234567') // 0701234567
```

### AreEqual

```js
areEqual(string, string): boolean
```

Cleans up provided strings and checks if the two phone number values match.

#### Example

```js
import { areEqual } from 'telefonnummer'

areEqual('0701234567', '0701234567') // true
areEqual('070-123.45 67', '070123--45 67') // true
```

### Tests

```
npm test
```
