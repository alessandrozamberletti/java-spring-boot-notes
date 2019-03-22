# @Configuration

* config.yml
```yml
node:
  value_single: "value1"
  value_array: "value1, value2, value3, value4"
  value_group:
    value_map:
      key1: "value1"
      key2: "value2"
      key3: "value3"
    value_single: "value1"
```

* under config/properties
```java
@Configuration
@ConfigurationProperties(prefix = "node")
public class SampleProperties {

    private String valueSingle;
    private List<String> valueArray = new ArrayList<>();
    private ValueGroup valueGroup;

    public static class ValueGroup {
        private Map<String, String> valueMap = new HashMap<>();
        private String valueSingle;
    }
}
```
