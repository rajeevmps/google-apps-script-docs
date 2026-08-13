# FieldType

An enum that defines the types that can be set for a Field.

An enum that defines the types that can be set for a `Field`. To use it, call `DataStudioApp.FieldType.PROPERTY_NAME`.

## Properties (Enum Values)

### Date/Time Types

| Property | Description |
|----------|--------------|
| `YEAR` | Year in the format of YYYY such as 2017. |
| `YEAR_QUARTER` | Year and quarter in the format of YYYYQ such as 20171. |
| `YEAR_MONTH` | Year and month in the format of YYYYMM such as 201703. |
| `YEAR_WEEK` | Year and week in the format of YYYYww such as 201707. |
| `YEAR_MONTH_DAY` | Year, month, and day in the format of YYYYMMDD such as 20170317. |
| `YEAR_MONTH_DAY_HOUR` | Year, month, day, and hour in the format of YYYYMMDDHH. |
| `YEAR_MONTH_DAY_MINUTE` | Year, month, day, hour, and minute in the format of YYYYMMDDHHmm. |
| `YEAR_MONTH_DAY_SECOND` | Year, month, day, hour, minute, and second in the format of YYYYMMDDHHmmss. |
| `QUARTER` | Quarter in the format of 1, 2, 3, or 4. |
| `MONTH` | Month in the format of MM such as 03. |
| `WEEK` | Week in the format of ww such as 07. |
| `MONTH_DAY` | Month and day in the format of MMDD such as 0317. |
| `DAY_OF_WEEK` | A number in the range of [0,6] with 0 representing Sunday. |
| `DAY` | Day in the format of DD such as 17. |
| `HOUR` | Hour in the format of HH such as 13. |
| `MINUTE` | Minute in the format of mm such as 12. |
| `DURATION` | A duration of time in seconds. |

### Geographic Types

| Property | Description |
|----------|--------------|
| `COUNTRY` | A country such as United States. |
| `COUNTRY_CODE` | A country code such as US. |
| `CONTINENT` | A continent such as Americas. |
| `CONTINENT_CODE` | A continent code such as 019. |
| `SUB_CONTINENT` | A sub-continent such as North America. |
| `SUB_CONTINENT_CODE` | A sub-continent code such as 003. |
| `REGION` | A region such as California. |
| `REGION_CODE` | A region code such as CA. |
| `CITY` | A city such as Mountain View. |
| `CITY_CODE` | A city code such as 1014044. |
| `METRO` | A metro such as San Francisco-Oakland-San Jose CA. |
| `METRO_CODE` | A metro code such as 200807. |
| `LATITUDE_LONGITUDE` | A latitude longitude pair such as 51.5074, -0.1278. |

### Basic Types

| Property | Description |
|----------|--------------|
| `NUMBER` | A decimal number. |
| `PERCENT` | Decimal percentage (can be over 1.0). For example, 137% is 1.37. |
| `TEXT` | Free-form text. |
| `BOOLEAN` | A `true` or `false` boolean value. |
| `URL` | A URL as text such as https://google.com. |

### Special Types

| Property | Description |
|----------|--------------|
| `HYPERLINK` | For calculated fields with the HYPERLINK function only. |
| `IMAGE` | For calculated fields with the IMAGE function only. |
| `IMAGE_LINK` | For calculated fields with HYPERLINK using IMAGE for link label. |

### Currency Types

Each currency is exposed as `CURRENCY_<CODE>` (e.g. `CURRENCY_USD`, `CURRENCY_EUR`). The documented currency codes are:

AED, ALL, ARS, AUD, BDT, BGN, BOB, BRL, CAD, CDF, CHF, CLP, CNY, COP, CRC, CZK, DKK, DOP, EGP, ETB, EUR, GBP, HKD, HRK, HUF, IDR, ILS, INR, IRR, ISK, JMD, JPY, KRW, LKR, LTL, MNT, MVR, MXN, MYR, NGN, NOK, NZD, PAB, PEN, PHP, PKR, PLN, RON, RSD, RUB, SAR, SEK, SGD, THB, TRY, TWD, TZS, UAH, USD, UYU, VEF, VND, YER, ZAR
