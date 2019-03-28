# Testing the web layer

```java
@Service
public class GreetingService {
    public String greet() {
        return "Hello World";
    }
}
```

```java
@Controller
public class GreetingController {

    private final GreetingService service;

    public GreetingController(GreetingService service) {
        this.service = service;
    }

    @RequestMapping("/greeting")
    public @ResponseBody String greeting() {
        return service.greet();
    }

}
```

```java
@RunWith(SpringRunner.class)
@WebMvcTest(GreetingController.class)
public class WebMockTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private GreetingService service;

    @Test
    public void greetingShouldReturnMessageFromService() throws Exception {
        when(service.greet()).thenReturn("Hello Mock");
        this.mockMvc.perform(get("/greeting")).andDo(print()).andExpect(status().isOk())
                .andExpect(content().string(containsString("Hello Mock")));
    }
}
```

* @MockBean creates and injects a mock for the GreetingService, and we set its expectations using Mockito
* @WebMvcTest is used to narrow down the tests to just the web layer

## References

* https://spring.io/guides/gs/testing-web/
