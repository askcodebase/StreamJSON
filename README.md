# StreamJson Format 

# Specifications

1. The StreamJson format is developed based on standard JSON. 

2. This format supports two types of elements which are JSON data and streaming text. 

3. These two types, JSON data and streaming text, are separated by the Unicode symbol '┄'.

4. In this format, JSON values can contain '@ref' as an identifier or reference to the corresponding streaming text.

5. A single JSON with one stream text is supported in this format. The JSON block precedes the Unicode symbol separator (which separates JSON and streaming text) followed by the streaming text block.

6. Multiple JSONs is also supported in this new format. Each JSON block precedes the Unicode symbol separator and follows with the connected streaming text. Afterward, it follows with another Unicode symbol separator to separate between another set of JSON-streaming text.

7. The JSON block is composed of key-value pairs conforming to the structure of standard JSON. 

8. The "streaming text" typically represents code blocks or large chunks of text data that are referenced in the JSON block.

9. Each instance of '@ref' in a JSON block corresponds to the streaming text that immediately follows it after the Unicode symbol separator. The '@ref' acts as a placeholder in the JSON, which gets replaced by the actual content from the streaming text during processing.

10. If there are multiple '@ref' instances in a JSON block, they correspond to different streaming text blocks, each separated by the Unicode symbol separator.

11. Only one '@ref' is allowed per json-object for referencing to one streaming text.

12. The Unicode symbol separator should not be used within the body of the JSON or streaming text. If it needs to be included, it should be properly escaped to avoid causing errors in parsing.

# Examples

1. One JSON with one streaming text

```javascript
{
  "createCodeSymbol": {
    "symbol": {
      "name": "Quicksort",
      "kind": 11,
      "content": "@ref"
    },
    "relativePosition": "endOfFile"
  }
}
┄
def quicksort(arr):
  if len(arr) <= 1:
    return arr
  pivot = arr[len(arr) // 2]
  left = [x for x in arr if x < pivot]
  middle = [x for x in arr if x == pivot]
  right = [x for x in arr if x > pivot]
  return quicksort(left) + middle + quicksort(right)
```
