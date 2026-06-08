## Description

There is a stream of `n` (idKey, value) pairs arriving in an arbitrary order, where `idKey` is an integer between `1` and `n` and `value` is a string. No two pairs have the same id.

Design a stream that returns the values in increasing order of their IDs by returning a chunk (list) of values after each insertion. The concatenation of all the chunks should result in a list of the sorted values.

Implement the `OrderedStream` class:

- `OrderedStream(int n)` — Constructs the stream to take `n` values.
- `String[] insert(int idKey, String value)` — Inserts the pair `(idKey, value)` into the stream, then returns the largest possible chunk of currently inserted values that appear next in the order.

## Code (Java)

```java
class OrderedStream {
    private int currIndex = 1;
    private String[] streamData;

    public OrderedStream(int n) {
        streamData = new String[n+1];
    }
    
    public List<String> insert(int idKey, String value) {
        streamData[idKey] = value;
        List<String> result = new ArrayList<>();

        while(currIndex < streamData.length && streamData[currIndex] != null){
            result.add(streamData[currIndex]);
            currIndex++;
        }
        return result;
    }
}

/**
 * Your OrderedStream object will be instantiated and called as such:
 * OrderedStream obj = new OrderedStream(n);
 * List<String> param_1 = obj.insert(idKey,value);
 */
```