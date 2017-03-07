# SpringBoot的helloworld

## 参考

http://www.cnblogs.com/ityouknow/p/5662753.html

## 区别:

1. 单元测试

从SpringBoot 1.4开始，unit test的annotation发生改变。

文章给出的是：
```java
@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(classes = MockServletContext.class)
@WebAppConfiguration
public class HelloWorldControlerTests {

    private MockMvc mockMvc;

    @Before
    public void setUp() throws Exception {
        mockMvc = MockMvcBuilders.standaloneSetup(new HelloWorldController()).build();
    }

    @Test
    public void getHello() throws Exception {
        //test using mockMvc
    }
}
```

1.4后变为
```java
@RunWith(SpringRunner.class)
@SpringBootTest
@AutoConfigureMockMvc
public class HelloWorldControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void testIndex() throws Exception {
        //test using mockMvc
    }
}
```