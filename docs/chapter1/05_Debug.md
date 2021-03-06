排错指引
===

一般常见会有几种错误，简单的判断错误方法就是判断状态码(`status_code`).

- `20x` 为成功状态
- `40x` 为受限服务，比如`404`没有找到资源，`401`，`403` 没有权限。
- `50x` 不用说了，服务器端错误。可以忽略，或者联系我修正。

一般的错误提示都会一个`json`里。

一种正常情况格式如下(如下例)：
```json
{
    "detail": "你要找的内容不存在。"
}
```

### 状态码说明


| 状态码 |状态| 方法 | 描述 |
| -- | -|- |--|
|200 | OK | [GET]| 服务器成功返回用户请求的数据，该操作是幂等的(Idempotent)。|
|201| CREATED| [POST/PUT/PATCH]|用户新建或修改数据成功。|
|202 |Accepted | [*]|表示一个请求已经进入后台排队（异步任务）
|204 |NO CONTENT | [DELETE]|用户删除数据成功。|
|400 |INVALID REQUEST | [POST/PUT/PATCH]|用户发出的请求有错误，服务器没有进行新建或修改数据的操作，该操作是幂等的。|
|401| Unauthorized | [*]|表示用户没有权限（令牌、用户名、密码错误）。|
|403 |Forbidden| [*]| 表示用户得到授权（与401错误相对），但是访问是被禁止的。|
|404 |NOT FOUND | [*]|用户发出的请求针对的是不存在的记录，服务器没有进行操作，该操作是幂等的。|
|406|Not Acceptable| [GET]|用户请求的格式不可得（比如用户请求JSON格式，但是只有XML格式）。|
|410| Gone|[GET]|用户请求的资源被永久删除，且不会再得到的。|
|422| Unprocesable entity| [POST/PUT/PATCH]| 当创建一个对象时，发生一个验证错误。|
|500 |INTERNAL SERVER ERROR | [*]|服务器发生错误，用户将无法判断发出的请求是否成功。|
