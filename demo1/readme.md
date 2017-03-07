# SpringBoot的helloworld

## 参考

http://www.cnblogs.com/ityouknow/p/5662753.html

## 区别:

### 1. 单元测试

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

### 2. 开发环境热加载

通过配置热加载，开发的时候一旦classpath下的class发生变化，servlet容器会自动重新加载，节省debug时间。

但IDEA不支持debug时自动编译，所以如果是从IDEA直接启动debug，修改后需要手动编译（Ctrl+F9），编译后servlet容器会自动加载变更的类。