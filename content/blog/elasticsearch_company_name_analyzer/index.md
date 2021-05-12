# Elasticsearch Company Name Analyzer

```jsx
{
    "settings": {
        "analysis": {
            "filter": {
                "company_name_harish": {
                    "type": "word_delimiter",
                    "generate_word_parts": false,
                    "generate_number_parts": true,
                    "catenate_words": true,
                    "preserve_original": true,
                    "stem_english_possessive": true
                },
                "elision": {
                    "type": "elision",
                    "articles_case": false,
                    "articles": [
                        "s"
                    ]
                }
            }
        }
    }
}
```

```shell
curl -X POST \
  http://localhost:9200/_analyze \
  -d '{
  "tokenizer" : "whitespace",
  "filter":  [ "asciifolding", "company_name_harish" ],
  "text":      "macy'\''s incorporated"
}'
```
