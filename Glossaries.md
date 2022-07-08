# DeepL Glossaries

## Outline <!-- omit in toc -->
* [Example Variables](#example-variables)
* [Creating a Glossary](#creating-a-glossary)
* [Verify by Getting a List of Glossaries](#verify-by-getting-a-list-of-glossaries)
* [Run a Translate Test with Glossary](#run-a-translate-test-with-glossary)
* [Listing entries of a glossary](#listing-entries-of-a-glossary)
* [Delete Glossary](#delete-glossary)
* [Update Glossary?](#update-glossary)
* [Reference](#reference)

## Example Variables

* `glossary_id`
  * Shortened example = `def3a26b-...`
  * Actual example = `def3a26b-3e84-45b3-84ae-0c0aaf3525f7`
* `creation_time`
  * Shortened example = `"2021-08-03T14..."`
  * Actual example = `"2021-08-03T14:16:18.329Z"`

## Creating a Glossary

Command:

| Parameter       | Value                              | Notes                    |
| --------------- | ---------------------------------- | ------------------------ |
| name*           | `Test`                             | Glossary Name            |
| source_lang*    | `ja`                               | Source texts' language   |
| target_lang*    | `en`                               | Target texts' language   |
| entries*        | `期間限定,Limited Time Offer"'!'"` | Glossary's entries       |
| entries_format* | `csv`                              | Data format (csv or tsv) |

⚠️ Make sure to put special characters in single & double quotes

```shell
curl "https://api.deepl.com/v2/glossaries" \
  --header "Authorization: DeepL-Auth-Key [yourAuthKey]" \
  --data-urlencode "name=Test" \
  -d "source_lang=ja" \
  -d "target_lang=en" \
  --data-urlencode "entries=期間限定,Limited Time Offer"'!'"" \
  -d "entries_format=csv"
```

Example Result:

```json
{
  "glossary_id": "def3a26b-...",
  "name": "Test",
  "ready": true,
  "source_lang": "ja",
  "target_lang": "en",
  "creation_time": "2021-08-03T14...",
  "entry_count": 1
}
```

## Verify by Getting a List of Glossaries

Command:

```shell
curl "https://api.deepl.com/v2/glossaries" \
  --header "Authorization: DeepL-Auth-Key [yourAuthKey]"
```

Example Response:

```json
{
  "glossaries": [{
    "glossary_id": "def3a26b-...",
    "name": "Test",
    "ready": true,
    "source_lang": "ja",
    "target_lang": "en",
    "creation_time": "2021-08-03T14...",
    "entry_count": 1
  }]
}
```

## Run a Translate Test with Glossary

```shell
curl https://api.deepl.com/v2/translate \
  -d auth_key= [yourAuthKey] \
  -d "text=期間限定"  \
  -d "source_lang=ja"  \
  -d "target_lang=en"  \
  -d "glossary_id=def3a26b-..."
```

## Listing entries of a glossary

Command:
* ⚡ Swap `[GLOSSARY_ID]` with your `glossary_id`
* ⚡ Only TSV or `tab-separated-values` is supported

```shell
curl "https://api.deepl.com/v2/glossaries/[GLOSSARY_ID]/entries" \
  --header "Accept: text/tab-separated-values" \
  --header "Authorization: DeepL-Auth-Key [yourAuthKey]"
```

## Delete Glossary

Command:

```shell
curl "https://api.deepl.com/v2/glossaries/64de1443-1d17-4247-bb8b-629e6b5c6978" \
 --request DELETE \
 --header "Authorization: DeepL-Auth-Key [yourAuthKey]"
```

Example Response: none

## Update Glossary?

As of July, 2022, there is no API to update a glossary.

It is recommended that a new glossary is made and delete the old glossary.

## Reference

* Docs: [Managing glossaries - DeepL API](https://www.deepl.com/en/docs-api/managing-glossaries/)
