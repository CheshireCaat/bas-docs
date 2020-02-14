## JSON Module Documentation

- JPath is the equivalent of XPath, which can be applied to data in JSON format. It works on the same principle, but not all of the XPath features are available in this case. The reason is that JSON is a more primitive data structure than Xml.
- For example, we cannot refer to the attributes of the elements, because in JSON they simply do not exist. But we can also search by conditions, use indexing and other features.
- The resulting variable can contain a simple value (**string**, **number**, **boolean**) or an array, which is a found element with all its fields.
- The **null** value can also be in an array in the case of a using action **Get Key** or **Get Keys**, if one of the sub-elements in turn represents the array itself.
- If the multiple query failed, the variables will contain **null** values.
- If the single query failed, the variable will contain **null** value.

## Example

```javascript
{
    "store": {
        "book": [
            {
                "category": "reference",
                "author": "Nigel Rees",
                "title": "Sayings of the Century",
                "price": 8.95
            },
            {
                "category": "fiction",
                "author": "Evelyn Waugh",
                "title": "Sword of Honour",
                "price": 12.99
            },
            {
                "category": "fiction",
                "author": "Herman Melville",
                "title": "Moby Dick",
                "isbn": "0-553-21311-3",
                "price": 8.99
            },
            {
                "category": "fiction",
                "author": "J. R. R. Tolkien",
                "title": "The Lord of the Rings",
                "isbn": "0-395-19395-8",
                "price": 22.99
            }
        ],
        "bicycle": {
            "color": "red",
            "price": 19.95
        }
    },
    "expensive": 10
}
```

| JsonPath | Result |
| :------- | :----- |
| $.store.book[*].author                | The authors of all books                                     |
| $..author                             | All authors                                                  |
| $.store.*                             | All things, both books and bicycles                          |
| $.store..price                        | The price of everything                                      |
| $..book[2]                            | The third book                                               |
| $..book[-2]                           | The second to last book                                      |
| $..book[0,1]                          | The first two books                                          |
| $..book[:2]                           | All books from index 0 (inclusive) until index 2 (exclusive) |
| $..book[1:2]                          | All books from index 1 (inclusive) until index 2 (exclusive) |
| $..book[-2:]                          | Last two books                                               |
| $..book[2:]                           | Book number two from tail                                    |
| $..book[?(@.isbn)]                    | All books with an ISBN number                                |
| $.store.book[?(@.price < 10)]         | All books in store cheaper than 10                           |
| $..book[?(@.price <= $['expensive'])] | All books in store that are not "expensive"                  |
| $..*                                  | Give me every thing                                          |

## Helpful links

- [JPath Syntax and Examples](https://goessner.net/articles/JsonPath/)
- [JPath Online Constructor](http://jsonpathfinder.com/) 
- [JPath Online Evaluator](http://jsonpath.com/)
