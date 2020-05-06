随着互联网技术的发展，微服务架构已经成为每个互联网公司的标配。伴随着服务粒度的细化，服务的安全和鉴权问题，以及客户端与服务之间的认证问题已经成为必不可少的一项工作。说起认证和鉴权，那怎么少得了 OAuth 2.0 协议呢？

火锅店旁边的照片打印机
这个案例想必大家都遇到过，在商场里面或者餐馆门口会看到一些可以打印照片的设备。想要设备打印出照片那么必须传输照片给设备，但是假如此时由于你的手机设备存储有限，美美的照片被存储在了百度云盘。那么如何让设备获取到你存储在云盘的照片呢？聪明的你肯定已经想到对策了。

1. 账户和密码

这种方式最为简单直接，但是一旦你将账户和密码告诉第三种应用，第三方应用就会无所不能，随意操作你的账户不受你的管控。你唯一能做的就是更改掉旧的密码，这样才能收回你的权限。

2. 开发者钥匙

这种方式需要先在资源提供方申请开发者钥匙，它建立在客户应用和资源方是互相信任的情况下。但是这种方式也会存在开发者钥匙泄露的情况，一旦泄露给不法分子，安全同样会受到威胁。

3. 特殊令牌

这种方式是资源方提供一个令牌给客户应用，通过令牌，客户应用可以访问资源。但是资源方颁发的令牌会受到权限的控制，并且会在有效期终止后自动销毁。

上述特殊令牌的方式即为我们今天即将要讨论的 OAuth 2.0，OAuth 2.0 会解决令牌涉及到的一系列问题。那么 OAuth 2.0 的令牌可以用来解决哪些问题呢？

开放系统间的授权
1. 社交联合登录

想必你在登录一个网站或者应用时候，一定遇到可以通过第三方的应用账户登录的案例。例如你在给一些技术博客做评论的时候需要登录，你又没有该博客的账户，但是你可以通过 GitHub 账户登录然后评论。

2. 开放接口平台

还是 GitHub 的例子，你不但可以直接去 GitHub 的网站上操作账户，你也可以通过 GitHub 提供的开放 API 来操作你的 GitHub 账户。有兴趣可以去了解一下：GitHub API。

微服务安全问题
微服务将应用拆成多个小的应用接口服务，但是各个服务之间的业务难免会有所依赖，此时服务之间的调用也需要有安全的保证。同时客户端的接入也会变得复杂，例如：单页面应用、原生应用、Web App 等。这些应用的接入都需要得到安全保证，OAuth 2.0 可以帮助我们解决这些问题。

内部应用授权
企业内部应用繁多，例如代码平台、应用发布平台、OA 系统等。如果为这些系统分别都创建一个账户，那么这对我们员工来说将是一个灾难，我们要记住每个账户和密码，每个系统都需要分别登录。因此有点规模的企业都需要一套单点登录的服务，我们可以通过 OAuth 2.0 来实现企业级的 SSO（单点登录） 服务。

初步认识 OAuth 2.0
如下图所示，OAuth 2.0 中包含四个重要的参与者：资源拥有者、客户应用、受保护资源、授权服务器。下面我们就详细说说 OAuth 2.0 的工作流程，它主要分为以下几个步骤：

![架构设计图](https://images.gitbook.cn/984c9360-cf1c-11e9-af41-f5624add887e)

首先资源拥有者在客户应用中发起对受保护资源的访问请求。
客户应用向资源服务器发起授权请求。
资源拥有者通过客户应用代理授予客户应用访问资源的权限。
授权服务器得到资源拥有者的指令，向客户应用颁发访问令牌。
客户应用获得受限的权限令牌，访问受保护的资源。
如上几个步骤即为 OAuth 2.0 的主要工作流程。当然其中还有少许细节，客户应用在获得令牌后，第二次访问资源就可以直接使用第一次获取的令牌来访问，无需再次获取。当然令牌也会过期，过期后客户应用需要重新获取授权，这是不是听起来很麻烦呢？OAuth 2.0 支持刷新令牌，即客户应用在令牌过期后，可以直接使用刷新令牌获得新的令牌，这样就省去了重新授权的复杂过程。

OAuth2 到底是什么
定义
上面我们介绍了 OAuth 2.0 的应用场景，以及它的工作流程，是时候来给出 OAuth 2.0 的定义了。

OAuth 2.0 是一个基于令牌 Token 的授权协议，通过它我们可以在不暴露账户和密码的情况下授予客户应用有限的数据访问权限。它解藕了认证和授权，同时它是事实上的安全框架，它能支持服务与服务，App、单页面应用与后端服务等很多应用场景。

授权模式
OAuth 2.0 共有如下四种授权模式，通过下面的任意一种方式，客户应用都可以获得授权令牌来访问受保护的资源。

授权码模式

这种方式是最复杂但也是最安全的方式。资源所有者授予客户应用访问权限后，授权服务器首次发放给客户应用的是一个授权码，随后客户应用在服务器端直接向授权服务器发起兑换授权令牌请求，这样才会获得真正的访问令牌。这种方式虽然复杂，但是你注意到访问令牌是客户应用服务器端代码直接发起的操作，并未通过终端代理，它提高了授权令牌的安全性。一般用于 Web 应用或者原生 App，这样 Token 就不会经过浏览器和 App，这样大大降低了 Token 泄漏的风险。

简化模式

这种方式是授权码模式的一个简化版本，资源所有者授权后，授权服务器直接将令牌发放至代理终端（例如浏览器），省去了授权码的流程。这种方式一般用于没有服务器的单页面应用，因为他们没有服务器端去拿授权码换取 Token。

密码模式

这种方式是资源拥有者直接将账户和密码告诉客户应用，客户应用使用账户和密码去授权服务器换取 Token。这种模式一般应用于企业内部的应用，应用之间是完全可信的，都是第一方应用。

客户端模式

这种方式是最简单的方式，同时它也是最不安全的方式。只要客户端发起请求，授权服务器即授予令牌。因此我们必须保证客户端的安全性，所以这种方式一般应用于企业内部的服务器、服务之间，它们之间无用户参与。

通过对四种工作模式的介绍，想必你已经明白了它们之间的区别，同时你也知道了它们具体的应用场景。最后我们将模式的选择总结如下图示：

![流程图](https://images.gitbook.cn/b59b0460-cf1c-11e9-956a-e59402c7f15a)

参照如上选择流程选择对应的应用模式，相信你已经掌握了如何选择合适的模式。

Spring Security OAuth 2.0 的架构设计
如下图所示，Spring Security OAuth2 主要设计了如下几个关键类来实现 OAuth 2.0 协议。下面我们来一一介绍它们。

![架构设计图](https://images.gitbook.cn/c1d05280-cf1c-11e9-956a-e59402c7f15a)

首先用户通过代理应用访问资源服务器，此时代理服务器发现尚未获取到授权信息，于是开始第二步访问授权服务器。
Spring Security OAuth 2.0 中提供的 AuthorizationEndpoint 为授权服务器开放了端点 /oauth/authorize，通过该端点用户代理可以将授权提示展示给用户。
用户选择授权范围然后确认，授权服务器根据用户代理提供的跳转地址将授权 Token 投递给用户代理，或者用户代理通过 /oauth/token 端点亲自获得 Token（这取决于你采用哪种工作模式）。
用户代理获取到 Token 以后携带 Token 信息访问资源服务器，资源服务器获取请求中包含的 Token 信息，然后将 Token 信息发送到授权服务器中 CheckTokenEndpoint 提供的 /oauth/check_token 端点以校验 Token 的真伪，校验通过后才准许用户代理访问授权的资源的。
当然了，Spring Security OAuth 2.0 允许我们定制自己的授权服务器和资源服务器，框架提供了如下 2 个接口。

AuthorizationServerConfigurer

该接口提供了如下三个方法来帮助你完成授权服务器的定制。

>void configure(AuthorizationServerSecurityConfigurer security) throws Exception; 该方法可以设置获取/校验 Token 端点的开放信息、密码的编码方式，以及是否需要 HTTPS 方式访问等。
void configure(ClientDetailsServiceConfigurer clients) throws Exception; 该方法用来配置用户信息资源，例如是存储在内存中或者数据库中，下文中我们会使用内存模式来演示案例。
void configure(AuthorizationServerEndpointsConfigurer endpoints) throws Exception; 该方法用来配置 Token 的生成模式，默认情况下我们不需要做配置，除非你需要开启 Password 模式或者你要接入 JWT Token。
ResourceServerConfigurer

该接口提供了如下二个方法帮我你完成资源服务器定制。

>void configure(ResourceServerSecurityConfigurer resources) throws Exception; 该方法用来配置资源服务器与授权服务器的一些交互信息，例如资源 ID 以及 Token 的鉴别配置。
void configure(HttpSecurity http) throws Exception; 该方法用来配置需要保护资源的 URI，以及哪些资源端点需要过排除在外。
经过上述基础架构的介绍，相信你已经有了大概的了解，但还是有些抽象对不对？接下来让我们用代码来实战一下吧。

Spring Security OAuth2 实战
本小节中，我们使用 Spring Boot 来分别构建我们的授权服务器、资源服务器、客户代理。

>授权服务器
我们使用 Maven 来构建 Spring Boot 项目，首先项目添加如下依赖：
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.security.oauth</groupId>
    <artifactId>spring-security-oauth2</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-jwt</artifactId>
</dependency>   
```
添加好依赖后，我们设置授权服务器，新建如下配置类：
```
@Configuration
@EnableAuthorizationServer
public class AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter {

    @Autowired
    private DataSource dataSource;

    @Override
    public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
    // 为了演示方便，此处我们使用内存模式来创建了 client 和 secret,  并且设置了授权服务器支持四种授权模式，如下  
        clients.inMemory().withClient("client").secret("secret")
                .authorizedGrantTypes("authorization_code", "implicit", "password", "client_credentials");
    }

    @Override
    public void configure(AuthorizationServerSecurityConfigurer security) throws Exception {
    // 设置授权服务器为所有人开放 token 校验端点：/oauth/check_token
        security.checkTokenAccess("permitAll()");
    }
}
```
如上我们使用注解 @EnableAuthorizationServer 就完成了一个简单的授权服务器。由于 Spring Security OAuth 2.0 是基于 Spring Security 框架来实现的，因此授权服务器中引入了 Security 的包，一旦引入此依赖包，授权服务器的所有端点也将受到 Spring Security 的安全保护。因此我们还需要对安全规则进行配置如下：
```
@Configuration
@EnableWebSecurity
public class WebSecurity extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
    // 配置使用 form 表单方式校验用户
        http.formLogin();
    }

    @Autowired
    public void configGlobal(AuthenticationManagerBuilder auth) throws Exception {
       // 创建用户，此处为了演示方便我们使用内存方式创建了用户：user，密码：password 
       auth.inMemoryAuthentication().withUser("user").password("password").roles("USER");
    }
}
```
资源服务器
创建好授权服务器以后，我们来创建资源服务器。同样简单，同上面引入相同的 POM 依赖信息，然后新建资源配置类：
```
@Configuration
@EnableResourceServer
public class ResourceServer extends ResourceServerConfigurerAdapter {

    @Override
    public void configure(HttpSecurity http) throws Exception {
    // 设置受保护的资源
        http.authorizeRequests()
                .antMatchers("/api/**").authenticated();
    }

    @Bean
   public ResourceServerTokenServices tokenServices() {
   // 创建远程 Token 校验服务，注意以下为了演示方便，hardcode 了 client，secret
       RemoteTokenServices tokenServices = new RemoteTokenServices();
       tokenServices.setCheckTokenEndpointUrl("http://localhost:8080/oauth/check_token");
       tokenServices.setClientId("client");
       tokenServices.setClientSecret("secret");
       tokenServices.setTokenName("token");
       return tokenServices;
   }

   @Bean
    public OAuth2AuthenticationManager authenticationManager() {
    // 创建认证管理器，并且制定 Token 校验服务
        OAuth2AuthenticationManager manager = new OAuth2AuthenticationManager();
        manager.setTokenServices(tokenServices());
        return  manager;
    }
}
```
如上我们已经完成了资源服务器的搭建，然后我们也设置了当资源服务器接收到客户代理的 Token 后如何向授权服务器发起 Token 校验。搭建好授权服务器与资源服务器以后就让我们来实战模拟一下吧。

授权码模式实战
获取授权码
我们使用浏览器来充当客户代理，发起获取 Token 请求。请求 URL 为：

http://localhost:8080/oauth/authorize?client_id=client&client_secret=secret&response_type=code&redirect_uri=http://localhost:9090/client/token/code&scope=user

注意上面的请求参数中：

>我们设置了 response_type=code 代表我们使用授权码模式；
redirect_uri=http://localhost:9090/client/token/code 代表授权服务器需要将授权码转发到我们客户应用制定的地址；
scope=user 代表用户需要授权的资源范围；
client_id=client&client_secret 代表客户代理应用的标识符。
请求后浏览器会跳转到校验用户的页面：

![1](https://images.gitbook.cn/24498530-cf1d-11e9-956a-e59402c7f15a)

输入我们在授权服务器中配置：user/password，然后点击 login 按钮。然后浏览器会输出要你选择是否同意授权。

![1](https://images.gitbook.cn/2d9547f0-cf1d-11e9-9620-ed84a236482a)

同意授权后即可看到浏览器跳转到了我们指定的跳转地址，并且携带了授权码参数 code。如下：

![1](https://images.gitbook.cn/37162470-cf1d-11e9-9cb8-a1abccba9727)

用授权码换取 Token
该操作是一个 Post 请求，我们借助于 Postman 工具来发起请求。URL 如下：

http://localhost:8080/oauth/token?scope=user&grant_type=authorization_code&code=HIEKoY&redirect_uri=http://localhost:9090/client/token/code
参数中发生变化的是 grant_type=authorization_code&code=HIEKoY，代表我们采用授权码方式获取 Token，并且附带了授权码参数 code。

Postman 示意图如下：

![1](https://images.gitbook.cn/3fcf4420-cf1d-11e9-9cb8-a1abccba9727)


需要注意的是，你需要在 PostMan 的 Authorization 标签栏目中输入用户校验信息，否则你无法通过 Spring Security 的安全校验。如下所示：

![2](https://images.gitbook.cn/48989070-cf1d-11e9-9620-ed84a236482a)

注意此时的校验信息为客户代理的标识符，不同于请求授权码时候输入的是资源拥有者的标识符。配置好请求信息后点击 Send 按钮发送请求，你会在 Postman 的请求结果栏目中获取到你想要的信息，类似如下：

{
    "access_token": "xxxx-yyyyy-mmmm-xxxx-dddd",
    "token_type": "bearer",
    "expires_in": 43199,
    "scope": "user",
    "jti": "05cefe4c-2e0e-41ec-811c-8a2633b83a2d"
}
携带 Token 访问资源
获取到 Token 以后我们就可以正常去访问资源了，如下我们设置 Token 即可完成请求。资源服务器接收到请求后，会拿我们提供的 Token 去授权服务器端校验，校验通过即访问成功。

![3](https://images.gitbook.cn/5a4085d0-cf1d-11e9-9cb8-a1abccba9727)

简化模式实战
简化模式省略掉了授权码的获取，可以直接去请求 Token，请求 URL 如下：

http://localhost:8080/oauth/authorize?client_id=client&client_secret=secret&response_type=token&redirect_uri=http://localhost:9090/client/token/code&scope=user
此时 response_type 参数值已经换成了 token，当然该有的用户验证还是必不可少。获取到 Token 以后之后的流程就和授权码一致了，在此就不重复了。

密码模式实战
相对于简化模式，密码模式需要使用账户和密码信息获得 Token，因此我们在请求 Token 的参数中需要加入账户的相关参数，如下：

http://localhost:8080/oauth/token?scope=user&grant_type=password&username=user&password=password
注意，此时 grant_type 变为了密码模式，并且多了 username 和 password 参数，获取到 Token 之后的流程同上面一致。

客户端模式实战
客户端模式就更简单了，只要请求就会获得 Token，如下：

http://localhost:8080/oauth/token?scope=user&grant_type=client_credentials
真实客户端代理
以上我们使用浏览器和 PostMan 来充当我们的客户代理，但是在实际项目中肯定不是这样玩的。实际客户代理都是开发好的程序，例如授权码模式，客户代理要先向授权服务器发起授权码的 HTTP 请求，然后在回调接口中完成 Token 的获取，获取到 Token 后再去请求用户的资源。我们只需要将上述实战中用浏览器和 PostMan 做的事情，交由程序去做就可以了，通常 Java 应用中我们使用 RestTemplate 完成这些操作。为此我也准备了 2 个范例代码：

SpringBoot 构建的服务器端 Web 项目客户代理
Android 开发的 Mobile 项目客户代理
基本运行原理我们都已经了如指掌了，代码实现比较简单，无非就是使用各终端的 HTTP 请求库帮我们完成 Token 的获取，以及完成相应的跳转。大家可以参考我的代码来实战一下，文章中就不占用过多代码内容了。代码 GitHub 仓库地址：Demo 仓库地址。

JWT 是什么？
JWT 全称 JSON Web Token，从名称上我们就可以看出它是一种 Token 令牌，那么它与我们上面说的 OAuth 2.0 提供的 Token 有什么区别呢。JWT 是一种自解释的加密 Token，在客户代理获取到的它的时候不需要再去授权服务器校验 Token 的有效性，资源服务器通过秘钥即可验证 Token，并且获取其中包含的信息。而我们上述使用到的 Token 是明文的，资源服务器收到 Token 后需要向授权服务器验证 Token 的有效性。当然 Spring Security OAuth 2.0 也可以集成 JWT，让我们来实战一下吧。

JWT 实战
改造授权服务器
首先我们为授权服务器加入 JWT 的依赖包：
```
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-jwt</artifactId>
</dependency>
```
其次我们只需要对，授权服务器的配置类稍作变动即可完成 JWT 的支持：
```
    @Autowired
    private AuthenticationManager authenticationManager;

// 将我们定义好的 token 生产方式设置到认证管理器中
    @Override
    public void configure(AuthorizationServerEndpointsConfigurer endpoints) throws Exception {
        endpoints.authenticationManager(authenticationManager)
                .tokenStore(tokenStore())
                .tokenEnhancer(jwtTokenEnhancer());
    }

    public TokenStore tokenStore() {
        return new JwtTokenStore(jwtTokenEnhancer());
    }
```
// 设置 JWT Token的签名钥匙，这里演示方便我们使用了对称加密，秘钥：123，这意味着解密这个 Token 也需要 123
```
    private JwtAccessTokenConverter jwtTokenEnhancer() {
        JwtAccessTokenConverter converter = new JwtAccessTokenConverter();
        converter.setSigningKey("123");
         return  converter;
    }
```
如上我们已经完成了授权服务器的改造，请求 Token 的操作流程与我们上面介绍的方式仍旧相同，不同的只是返回结果中 Token 变成了 JWT token。

改造资源服务器
同样资源服务器的 POM 依赖中同样需要加入 JWT 的依赖，参考上面。我们需要在资源服务器的配置类中告诉资源服务器如何去校验 Token，你一定记得未引入 JWT 时候，我们设置了 RemoteTokenServices，此时我们需要将它换为 JWT Token store。
```
 @Bean
 public TokenStore tokenStore() {
     return new JwtTokenStore(accessTokenConverter());
 }

// 设置如何解密 JWT token
 @Bean
 public JwtAccessTokenConverter accessTokenConverter() {
     JwtAccessTokenConverter converter = new JwtAccessTokenConverter();
     converter.setSigningKey("123");
     return converter;
 }
 @Bean
 @Primary
 public DefaultTokenServices tokenServices() {
     DefaultTokenServices defaultTokenServices = new DefaultTokenServices();
     defaultTokenServices.setTokenStore(tokenStore());
     return defaultTokenServices;
 }
 ```
如上我们就完成了资源服务器对 JWT 的支持，同样客户代理请求资源服务器的请求方式依然不变。只是本来的明文令牌，变成了现在加密 JWT 令牌。怎么样？是不是很简单呢，快去实践一下吧。你可以试着将加密方式换为非对称加密，这个就当做小作业留给大家吧。

社交登陆案例 GitHub（Spring Social）
Spring Social 是 Spring 的一个扩展项目，它帮助我们封装了很多社交登录平台的接口服务，当我们需要一些社交登录功能的时候使用它是非常方便的。它封装了很多平台的实现，例如 GitHub、微博、微信、Twitter、Facebook 等，感兴趣的同学可以去官网查看：Spring Social。接下来我们以 GitHub 为例简单介绍一下如何使用。

注册 GitHub 应用
首先你需要注册成为 GitHub 的受信任应用才可以进行之后的操作，访问 GitHub 创建项目。注册成功后你需要得到：Client ID 和 Client Secret 在项目中配置。如下所示：

![](https://images.gitbook.cn/4bf9c560-cf34-11e9-b7bb-e113b501764e)

引入 POM 依赖包
```
<dependency>
    <groupId>org.springframework.social</groupId>
    <artifactId>spring-social-config</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.social</groupId>
    <artifactId>spring-social-core</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.social</groupId>
    <artifactId>spring-social-web</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.social</groupId>
    <artifactId>spring-social-github</artifactId>
    <version>1.0.0.M4</version>
</dependency>
```
注意上面的 spring-social-github 包，它才是具体的 GitHub 接口封装，上面的是 Spring Social 的抽象层，针对我们需要的不同社交登录平台，只需要更换实现包即可。

创建配置类
```
@Configuration
@EnableSocial
@EnableConfigurationProperties(GitHubProperties.class)
public class GitHubConfiguration extends SocialAutoConfigurerAdapter {

    private final GitHubProperties properties;

    public GitHubConfiguration(GitHubProperties properties) {
        this.properties = properties;
    }

// 加载 GitHub provider 
    @Bean
    @Scope(value = "request", proxyMode = ScopedProxyMode.INTERFACES)
    public GitHub gitHub(ConnectionRepository repository) {
        Connection<GitHub> connection = repository
                .findPrimaryConnection(GitHub.class);
        return connection != null ? connection.getApi() : null;
    }

// 启用框架设定好的端点，终端请求 /connect/{providerId} 触发后续操作：获取授权码，换取 Token 等流程。
    @Bean
    public ConnectController connectController(
            ConnectionFactoryLocator factoryLocator,
            ConnectionRepository repository) {

        ConnectController controller = new ConnectController(
            factoryLocator, repository);
        controller.setApplicationUrl("http://localhost:8080");
        return controller;
    }

// GitHub 连接工厂类，配置了我们第一步操作中获取到的 ID 和 秘钥
    @Override
    protected ConnectionFactory<?> createConnectionFactory() {
        return new GitHubConnectionFactory(properties.getAppId(),
                properties.getAppSecret());
    }
}
```
如上我们即完成了 Spring Social GitHub 的配置类。接下来我们要写一个服务端点来请求受保护资源：
```
@Autowired
private ConnectionRepository connectionRepository;

@GetMapping
public String repositories(Model model) {
// 进入应用后首先访问根路径，请求进来发现尚未获取到 GitHub 访问资源许可，跳转页面，展示下面的页面模板资源，由用户发起授权请求
    if (connectionRepository.findPrimaryConnection(GitHub.class) == null) {
        return "redirect:/connect/github";
    }

    String name = github.userOperations().getUserProfile().getName();
    String username = github.userOperations().getUserProfile()
            .getUsername();
    model.addAttribute("name", name);

    String uri = "https://api.github.com/users/{user}/repos";
    GitHubRepo[] repos = github.restOperations().getForObject(uri,
            GitHubRepo[].class, username);
    model.addAttribute("repositories", Arrays.asList(repos));

    return "repositories";
}
```
对应前端页面模板：
```
<html>
<head>
    <title>Social Authcode</title>
</head>
<body>
    <h2>Connect to GitHub to see your repositories</h2>
<!--点击按钮就会请求我们在配置类中启动的框架中包含的端点 /connect/github, 后面的操作就都被封装在框架中了-->
    <form action="/connect/github" method="POST">
        <input type="hidden" name="scope" value="public_repo user" />

        <div class="formInfo">
            Click the button to share your repositories with <b>social-github</b>
        </div>
        <p><button type="submit">Connect to GitHub</button></p>
    </form>

</body>
</html>
```
如上我们就使用 Spring Social 集成了 GitHub 的 OAuth 2.0 授权支持，在必要的地方都做了注释，应用运行的截图就不展示了，给偷懒的小朋友留个作业，快去实战一下吧。有困难的同学可以参考一下 Demo 源代码。

总结
本文首先介绍了 OAuth 2.0 协议的工作原理，以及四种工作模式。其次使用 Spring Security OAuth 2.0 完成了我们的代码实战部分，以及如何集成 JWT， 最后介绍了 Spring Social 框架的简单使用。

相信一步步跟着实战过来的小伙伴们已经都掌握了 OAuth 2.0 主要内容了，如果还有没看明白的地方欢迎留言给我一起来讨论吧。由于个人能力有限，文中难免有遗漏不足的地方，欢迎大家批评指正。

最后如果本文对你有所收获，欢迎点个赞给我吧，谢谢啦。也欢迎大家关注我的公众号“码农尼克”一起交流学习。

本文首发于 GitChat，未经授权不得转载，转载需与 GitChat 联系。