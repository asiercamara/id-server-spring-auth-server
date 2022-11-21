# 🚀Id Server
[Id Server](https://github.com/NotFound403/id-server) is an open source authorization based on [Spring Authorization Server](https://github.com/spring-projects/spring-authorization-server) The server pulls the code and runs it directly without too much configuration. Welcome to Star, if you are interested, you can also contribute to this project.
- github: [https://github.com/NotFound403/id-server](https://github.com/NotFound403/id-server)
- gitee: [https://gitee.com/felord/id-server](https://gitee.com/felord/id-server)
- Documentation under construction...
## The main function
- Works out of the box and requires only a small amount of configuration to use.
- Create and manage OAuth2 clients.
- Provide OAuth2 authorization service.
- Supports four client authentication methods:
  - **CLIENT_SECRET_BASIC**
  - **CLIENT_SECRET_POST**
  - **CLIENT_SECRET_JWT**
  - **PRIVATE_KEY_JWT**
- Support three OAuth2 authorization methods:
  - **AUTHORIZATION_CODE**
  - **CLIENT_CREDENTIALS**
  - **REFRESH_TOKEN**
- Supports the following user authentication methods:
  - account password login
  - Mobile phone number verification code login
  - Applet login
- **OIDC 1.0** support (in progress).
- Generate configuration `yaml` files with one click.
- Provide a UI console to reduce the cost of getting started.
- The user role of the administrator can be dynamically adjusted, and the authority control of the button function level can be performed on the authorization server.
## Environment and Technology
- Java 8 and above
- **Spring Boot**
- **Spring Security**
- **Spring Authorization Server**
- **Spring Data JPA**
- **pear admin layui**
- **thymeleaf**
- database
  - **H2**
  - **Mysql**

## Simple usage
- Pull the latest code from the main branch to the local.
- Start the authorization server with `IdServerApplication`. The local login path of the management console is `http://localhost:9000/system/login`, the highest authority user is `root`, and the password is `idserver`.
- You can do these things as `root` user:
  - Create roles (role management) and bind permissions to roles.
  - Create console management users (user management) and assign them roles.
> The exit function is not yet perfect, and the session needs to be cleared by closing the browser.
## OAuth2 test method
- Start **Id Server**, by default a built-in OAuth2 client is provided in the client list.
- The sample client is in the `samples` folder, start it directly, go to `http://127.0.0.1:8082/foo/bar` under the browser configuration file, enter the login page, and enter the user name `user` and password `user` will do.
- You can also create a client in Id Server and imitate the configuration in DEMO, mainly modify `client-id`, `client-secret`, `client-authentication-method`, `scope`, other options unless you compare Understand OAuth2, otherwise don't move, you can also consult through issue.
> `redirect-uri` must be declared when the authorization server Id Server registers the client.
### How to replace the built-in user user
First of all, it is necessary to correctly distinguish the two concepts of **management user** and **common user**.
#### Manage Users
`root` and the user it creates are the management users of the UI console. The super administrator `root` is currently provided as a default user with the highest authority of the Id Server. If you need to customize, you can implement the `RootUserDetailsService` interface and inject **Spring IoC**.
#### general user
Ordinary users are resource owners in OAuth2, mainly authorizing authorization requests from OAuth2 clients. By default, a `user` is provided for demonstration. Developers can implement the `OAuth2UserDetailsService` interface and inject **Spring IoC** to customize the source of users.
### Mobile number verification code login
Now OAuth2 authorization adds a mobile phone number verification code login, inspired by the []() extension package, which does not affect the original OAuth2 authorization process. The resource owner can choose the authentication method on the following page:
![](https://asset.felord.cn/blog/20220520111451.png)
#### Close verification code authentication method
For those who do not use the verification code authentication method, it can be adjusted through the `enableCaptchaLogin` parameter in the `OAuth2LoginController#oauth2LoginPage` interface, and the default value is `true` (on).
## surroundings
Currently **Id Server** provides **H2** and **Mysql** two database environments, corresponding to `application-h2.yml` and `application-mysql.yml` two configuration files.
- **H2**, the default database, in the **H2** environment, database DDL scripts and DML scripts will be executed automatically, without manual execution by developers, this environment is mainly used for testing, research, and learning.
- **Mysql**, recommended for production, **The developer manually executes the initialization DML script** when starting for the first time**.
> At present, the effects of the two environments are the same. If H2 takes a long time, tables will be lost. When switching, be sure to replace the corresponding database driver dependencies in `pom.xml`.
## screenshot
![Console login](https://asset.felord.cn/blog/20220512143700.png)
![Homepage](https://asset.felord.cn/blog/20220512134905.png)
![Create OAuth2 client through UI](https://asset.felord.cn/blog/20220512135204.png)
![Create management user](https://asset.felord.cn/blog/20220512135249.png)
![One-click configuration generation](https://asset.felord.cn/blog/20220513141607.gif)
![Role Authorization](https://asset.felord.cn/blog/20220512135420.png)
![Authorized login](https://asset.felord.cn/blog/20220512143317.png)
![Authorization confirmation](https://asset.felord.cn/blog/20220512143550.png)

