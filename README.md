## goauth2


Tested for Google, Facebook and Weibo.com. They work perfect.

To use it:

`go get github.com/arkxu/goauth2/oauth`

The change is based on weibo.com's defect about the callback which has `Content-Type: text/plain` in the header but has json format in the body.
They should send `application/json` content-type instead.

Have to fork my own until Weibo.com correct the problem.

Forked from http://code.google.com/p/goauth2/

### How to use

```Go
  var WeiboOAuthCfg *oauth.Config

  WeiboOAuthCfg = new(oauth.Config)
  WeiboOAuthCfg.ClientId = "your weibo.clientId"
  WeiboOAuthCfg.ClientSecret = "your weibo.clientSecret"
  WeiboOAuthCfg.Scope = "email,direct_messages_write,direct_messages_read"
  WeiboOAuthCfg.AuthURL = "https://api.weibo.com/oauth2/authorize"
  WeiboOAuthCfg.TokenURL = "https://api.weibo.com/oauth2/access_token"
  WeiboOAuthCfg.RedirectURL = "http://yourapp:port/yourcallback"

  loginUrl := WeiboOAuthCfg.AuthCodeURL("")
```

loginUrl is the URL your login link should point to in the view. The the callback handler code should look like

```Go
  t := &oauth.Transport{Config: WeiboOAuthCfg}
  tok, err := t.Exchange(code) // This is the code in url parameter back from weibo.com
  if err != nil {
    fmt.Println("something went wrong", err)
  }

  fmt.Println(tok.AccessToken) // This is the access token you are looking for!

```