# Elastic-Farsi-CharFilter
a Configuration of Creating an index contains Farsi-CharFilter

##Create Index

  PUT new_index
  {
    "settings": {
      "analysis": {
        "analyzer": {
          "my_analyzer": {
            "tokenizer": "standard",
            "char_filter": [
              "my_char_filter"
            ]
          }
        },
        "filter": {
        },
        "char_filter": {
          "my_char_filter": {
            "type": "mapping",
            "mappings": [
              "٠ => 0",
              "١ => 1",
              "٢ => 2",
              "٣ => 3",
              "٤ => 4",
              "٥ => 5",
              "٦ => 6",
              "۷ => 7",
              "۸ => 8",
              "٩ => 9",
              "۴ => 1",
              "۵ => 2",
              "۶ => 3",
              "ي => ی",
              "ك => ک",
              "ؤ => و" ,
              "ئ => ی",
              "أ => ا",
              "آ => ا",
              "إ => ا",
              "ۀ => ه",
              "ة => ه" 
            ]
          }
        }
      }
    }
  }

## Configure Mapping

  PUT new_book_test/_mapping
  {
    "properties": {
      "id": {
        "type": "text",
        "fields": {
          "ngram": {
            "type": "text",
            "analyzer": "my_analyzer"
          }
        }
      },
      "name": {
        "type": "text",
        "fields": {
          "ngram": {
            "type": "text",
            "analyzer": "my_analyzer"
          }
        }
      }
    }
  }
