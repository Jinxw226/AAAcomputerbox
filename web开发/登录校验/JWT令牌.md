#JWT令牌 
JWT令牌最典型的应用场景就是登录认证：
1. 在浏览器发起请求来执行登录操作，此时会访问登录的接口，如果登录成功之后，我们需要生成一个jwt令牌，将生成的 jwt令牌返回给前端。
2. 前端拿到jwt令牌之后，会将jwt令牌存储起来。在后续的每一次请求中都会将jwt令牌携带到服务端。
3. 服务端统一拦截请求之后，先来判断一下这次请求有没有把令牌带过来，如果没有带过来，直接拒绝访问，如果带过来了，还要校验一下令牌是否是有效。如果有效，就直接放行进行请求的处理。


在JWT登录认证的场景中我们发现，整个流程当中涉及到两步操作：
1. 在登录成功之后，要生成令牌。
2. 每一次请求当中，要接收令牌并对令牌进行校验。

# JWT令牌介绍

- JWT全称 JSON Web Token （官网：[JSON Web Tokens - jwt.io](https://jwt.io/)），定义了一种简洁的、自包含的格式，用于在通信双方以json数据格式安全的传输信息。由于数字签名的存在，这些信息是可靠的。
    
    - 简洁：是指jwt就是一个简单的字符串。可以在请求参数或者是请求头当中直接传递。
    - 自包含：指的是jwt令牌，看似是一个随机的字符串，但是我们是可以根据自身的需求在jwt令牌中存储自定义的数据内容。如：可以直接在jwt令牌中存储用户的相关信息。
    - 简单来讲，jwt就是将原始的json数据格式进行了安全的封装，这样就可以直接基于jwt在通信双方安全的进行信息传输了。

## JWT令牌组成

JWT的组成： （JWT令牌由三个部分组成，三个部分之间使用英文的点来分割）

- 第一部分：==Header(头）==， 记录令牌类型、签名算法等。 例如：{"alg":"HS256","type":"JWT"}
- 第二部分：==Payload(有效载荷）==，携带一些自定义信息、默认信息等。 例如：{"id":"1","username":"Tom"}
- 第三部分：==Signature(签名）==，防止Token被篡改、确保安全性。将header、payload，并加入指定秘钥，通过指定签名算法计算而来。

==签名的目的==
就是为了防jwt令牌被篡改，而正是因为jwt令牌最后一个部分数字签名的存在，所以整个jwt 令牌是非常安全可靠的。一旦jwt令牌当中任何一个部分、任何一个字符被篡改了，整个令牌在校验的时候都会失败，所以它是非常安全可靠的。

![[JWT令牌格式.png]]

JWT是如何将原始的JSON格式数据，转变为字符串的呢？

- 其实在生成JWT令牌时，会对JSON格式的数据进行一次编码：进行base64编码
- ==Base64==：是一种基于64个可打印的字符来表示二进制数据的编码方式。既然能编码，那也就意味着也能解码。所使用的64个字符分别是==A到Z、a到z、 0- 9，一个加号，一个斜杠==，加起来就是64个字符。任何数据经过base64编码之后，最终就会通过这64个字符来表示。当然还有一个符号，那就是等号。等号它是一个补位的符号
- 需要注意的是Base64是编码方式，而不是加密方式。

# 生成和校验JWT令牌

1).引入JWT的依赖：

```XML
<!-- JWT依赖-->
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.9.1</version>
</dependency>
```

在引入完JWT来赖后，就可以调用工具包中提供的API来完成JWT令牌的生成和校验。工具类：Jwts

2).生成JWT代码实现

```java
@Test  
public void testGenerateJwt(){  
    Map<String , Object> dataMap = new HashMap<>();  
    dataMap.put("id", "1");  
    dataMap.put("username", "admin");  
    //指定加密算法、密钥  
    String jwt = Jwts.builder().signWith(SignatureAlgorithm.HS256, "aXRqZg==")  
            .addClaims(dataMap)//添加自定义信息  
            .setExpiration(new Date(System.currentTimeMillis() + 1000 * 60 ))//设置过期时间  
            .compact();//生成令牌  
    System.out.println(jwt);  
}
```

运行测试方法：

```Java
eyJhbGciOiJIUzI1NiJ9.eyJpZCI6MSwiZXhwIjoxNjcyNzI5NzMwfQ.fHi0Ub8npbyt71UqLXDdLyipptLgxBUg_mSuGJtXtBk
```

3).解析JWT代码实现

```java
@Test  
public void testParseJwt(){  
    String token = "eyJhbGciOiJIUzI1NiJ9.eyJpZCI6IjEiLCJ1c2VybmFtZSI6ImFkbWluIiwiZXhwIjoxNzUyOTkxNjM1fQ.ixL6FXHtKbu1MI4obUhmT_m33NnpF3Ezx7pUhFa2U0U";  
    Claims claims = Jwts.parser().setSigningKey("aXRqZg==")//指定密钥  
            .parseClaimsJws(token)//解析令牌  
            .getBody();//获取自定义信息  
    System.out.println(claims);  
}
```

运行测试方法：

```Java
{id=10, username=itheima, exp=1701909015}
```


> [!NOTE]
> 通过以上测试，我们在使用JWT令牌时需要注意：
> - JWT校验时使用的签名秘钥，必须和生成JWT令牌时使用的==秘钥是配套的==。
> - 如果JWT令牌解析校验时报错，则说明 JWT令牌==被篡改== 或 ==失效了==，令牌非法。


# AI生成令牌实体类提示词：

请帮我基于如下单元测试方法，改造成一个JWT令牌操作的工具类，类名：JwtUtils，具体要求如下：
1.工具类中有两个方法，一个方法生成令牌，另一个是解析令牌
2.生成令牌时使用的密钥和测试类中一致即可
3.令牌的过期时间设置12小时
原始测试类代码如下：粘贴上面测试类的代码