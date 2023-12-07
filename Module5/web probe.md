Выбери сайт на который вы хотите подключить проверку

```
Name: Web test
Variables
  {login} <свой логин>
  {password} <свой пароль>

Steps

Step 1
  Name: First page
  URL: <Ваш сайт>

  Variables
    {token1} regex:name="_token" value="([0-9A-Za-z]{32})"
Можно проще:
    {token1} regex:name="_token" value="(.{32})"

  Required string: rcmloginsubmit
  Required status codes: 200
  
Step 2
  Name: Log in
  URL: <Ваш сайт>
  
  Post fields
    _token: {token1}
    _task: login
    _action: login
    _user: {login}
    _pass: {password}

  Variables
    {token2}: regex:name="_token" value="(.{32})"
    
  Follow redirects: YES
  
  Required string: button-logout
  Required status codes: 200
  
Step 3
  Name: Log out
  URL: <Ваш сайт>
  
  Query fields
    _task: logout
    _token: {token2}
    
  Required string: rcmloginsubmit
  Required status codes: 200

```
