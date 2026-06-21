# Encode and Decode TinyURL

TinyURL is a URL shortening service where you enter a URL such as `https://leetcode.com/problems/design-tinyurl` and it returns a short URL such as `http://tinyurl.com/4e9iAk`. Design a class to encode a URL and decode a tiny URL.

There is no restriction on how your encode/decode algorithm should work. You just need to ensure that a URL can be encoded to a tiny URL and the tiny URL can be decoded to the original URL.

Implement the `Solution` class:

- `Solution()` Initializes the object of the system.
- `String encode(String longUrl)` Returns a tiny URL for the given `longUrl`.
- `String decode(String shortUrl)` Returns the original long URL for the given `shortUrl`. It is guaranteed that the given `shortUrl` was encoded by the same object.

## Solution

```java
public class Codec {
    private Map<String, String> urlMapping = new HashMap<>();

    private int counter = 0;
    private static final String BASE_DOMAIN = "https://tinyurl.com/";

    // Encodes a URL to a shortened URL.
    public String encode(String longUrl) {
        String uniqueId = String.valueOf(++counter);
        urlMapping.put(uniqueId, longUrl);
        return BASE_DOMAIN + uniqueId;
    }

    // Decodes a shortened URL to its original URL.
    public String decode(String shortUrl) {
        int lastSlashIndex = shortUrl.lastIndexOf('/')+1;
        String uniqueId = shortUrl.substring(lastSlashIndex);
        return urlMapping.get(uniqueId);
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(url));
```