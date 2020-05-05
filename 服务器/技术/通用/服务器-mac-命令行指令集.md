# 结束指定端口进程指令
sudo lsof -i:20101
ps -ef|grep 9905
kill -9 9905
ps -ef|grep 9905 

```
//接受客户端返回的code，提交申请access token的请求

   @RequestMapping("/callbackCode")

   public Object toLogin(HttpServletRequestrequest)throws OAuthProblemException{

      System.out.println("-----------客户端/callbackCode--------------------------------------------------------------------------------");

      clientId = "clientId";

      clientSecret = "clientSecret";

      accessTokenUrl="http://localhost:8082/oauthserver/responseAccessToken";

       userInfoUrl = "userInfoUrl";

       redirectUrl = "http://localhost:8081/oauthclient01/server/accessToken";

       HttpServletRequest httpRequest = (HttpServletRequest)request;

       code = httpRequest.getParameter("code");

       System.out.println(code);

       OAuthClient oAuthClient =new OAuthClient(new URLConnectionClient());

       try {

        OAuthClientRequest accessTokenRequest = OAuthClientRequest

              .tokenLocation(accessTokenUrl)

                .setGrantType(GrantType.AUTHORIZATION_CODE)

                .setClientId(clientId)

                .setClientSecret(clientSecret)

                .setCode(code)

                .setRedirectURI(redirectUrl)

                .buildQueryMessage();

        //去服务端请求access token，并返回响应

        OAuthAccessTokenResponse oAuthResponse =oAuthClient.accessToken(accessTokenRequest, OAuth.HttpMethod.POST);

        //获取服务端返回过来的access token

        String accessToken = oAuthResponse.getAccessToken();

        //查看access token是否过期

            Long expiresIn =oAuthResponse.getExpiresIn();

            System.out.println("客户端/callbackCode方法的token：：："+accessToken);

            System.out.println("-----------客户端/callbackCode--------------------------------------------------------------------------------");

            return"redirect:http://localhost:8081/oauthclient01/server/accessToken?accessToken="+accessToken;

      } catch (OAuthSystemExceptione) {

        e.printStackTrace();

      }

       return null;

   }
```