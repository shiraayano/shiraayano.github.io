### RESTful 语法规范详解
在我们编写接口时，有一种语法风格规范，RESTful风格语法是http作者提出的一种。

RESTful 是一种基于 REST（Representational State Transfer）架构的 API 设计规范，广泛用于 Web 服务的设计和实现。它依赖于标准的 HTTP 协议，并使用资源的表述来提供服务。



RESTful的资源表现形式是XML或者JSON

### 1. **核心原则**
+ **资源**: 一切皆资源，资源通过 URI（统一资源标识符）表示。
+ **HTTP 方法**: 使用标准的 HTTP 方法定义操作行为。
    - `GET`: 获取资源。
    - `POST`: 创建资源。
    - `PUT`: 更新资源（整体更新）。
    - `PATCH`: 更新资源（部分更新）。
    - `DELETE`: 删除资源。
+ **无状态**: 每个请求从客户端到服务器必须包含完成请求所需的所有信息，服务器不保存客户端的上下文。
+ **表现层状态转移**: 服务器通过资源的表述（如 JSON 或 XML）来传递状态。
+ **统一接口**: 通过通用的、标准化的接口来操作资源。

### 2. **URI 设计规范**
+ **层次结构**: 使用路径来表示资源的层次关系。
+ **复数名词**: 资源名使用复数形式。
+ **小写字母**: URI 使用小写字母，单词间用连字符（-）分隔。
+ **无动作动词**: 不要在 URI 中包含操作或动词，操作由 HTTP 方法定义。

#### 示例：
+ 获取所有用户：`GET /users`
+ 获取单个用户：`GET /users/{id}`
+ 创建新用户：`POST /users`
+ 更新用户：`PUT /users/{id}`
+ 删除用户：`DELETE /users/{id}`

### 3. **HTTP 方法与状态码**
RESTful API 使用标准的 HTTP 方法和状态码来表示请求的结果。

+ **GET** 请求： 
    - 成功返回 `200 OK`
    - 资源不存在返回 `404 Not Found`
+ **POST** 请求： 
    - 成功创建返回 `201 Created`
    - 请求格式错误返回 `400 Bad Request`
+ **PUT** 请求： 
    - 成功更新返回 `200 OK` 或 `204 No Content`
    - 资源不存在返回 `404 Not Found`
+ **DELETE** 请求： 
    - 成功删除返回 `204 No Content`
    - 资源不存在返回 `404 Not Found`

### 4. **请求与响应格式**
通常，RESTful API 使用 JSON 格式进行数据交换，因为它易于解析和人类可读。

#### 请求示例：
创建新用户的 `POST` 请求：

```plain
POST /users HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "password": "securepassword"
}
```

#### 响应示例：
```plain
HTTP/1.1 201 Created
Location: /users/123
Content-Type: application/json

{
  "id": 123,
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

### 5. **分页与过滤**
RESTful API 应该支持分页和过滤，以避免一次性返回大量数据。

#### 示例：
获取第 2 页，每页 10 个用户：

```plain
GET /users?page=2&limit=10
```

按状态过滤用户：

```plain
GET /users?status=active
```

### 6. **版本控制**
为了保持兼容性和灵活性，RESTful API 通常包含版本信息。

#### 示例：
通过 URL 进行版本控制：

```plain
GET /v1/users
```

通过请求头进行版本控制：

```plain
GET /users
Accept: application/vnd.example.v1+json
```

### 7. **安全性**
+ **认证**: 使用 OAuth、JWT 或 API 密钥来认证用户。
+ **加密**: 使用 HTTPS 确保数据在传输过程中的安全。

### 8. **示例应用场景**
#### 示例 1: 获取所有文章
```plain
GET /articles HTTP/1.1
Host: api.example.com
```

响应：

```plain
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "title": "Introduction to RESTful APIs",
    "author": "Alice"
  },
  {
    "id": 2,
    "title": "Advanced RESTful Design",
    "author": "Bob"
  }
]
```

#### 示例 2: 创建新文章
```plain
POST /articles HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "title": "New API Features",
  "content": "Details about the new features in our API.",
  "author": "Charlie"
}
```

响应：

```plain
HTTP/1.1 201 Created
Location: /articles/3
Content-Type: application/json

{
  "id": 3,
  "title": "New API Features",
  "author": "Charlie"
}
```

RESTful 语法通过统一的接口和资源表述，使 API 设计更直观、标准化，便于客户端与服务器的交互。

#### 其它补充
##### http介绍
HTTP（Hypertext Transfer Protocol）本质上是一种**半双工**协议。这意味着在一次 HTTP 请求-响应周期中，通信是单向的：客户端（通常是浏览器或应用程序）发送请求，服务器接收到请求后处理并返回响应。在这个过程中，通信的方向是先从客户端到服务器，再从服务器到客户端，双方不能同时发送和接收数据。

### 半双工特性：
+ **单向通信**: 在任意时刻，数据只能在一个方向上传输，要么是客户端向服务器发送请求，要么是服务器向客户端发送响应。
+ **请求-响应模式**: 每个请求必须等待相应的响应完成后才能发起下一个请求。

### HTTP/2 和 HTTP/3 的改进
尽管传统的 HTTP/1.1 是半双工的，HTTP/2 和 HTTP/3 在这方面引入了一些改进，使其具有类似**全双工**的能力：

+ **多路复用（Multiplexing）**: 允许在一个连接中同时发送多个请求和接收多个响应，不需要按顺序等待前一个请求完成。尽管每个请求-响应仍然是半双工的，但可以并行处理多个流。
+ **流优先级**: 支持不同流的优先级管理，使关键请求可以更快得到响应。

### 全双工特性：
+ **同时通信**: 在任意时刻，客户端和服务器可以同时发送和接收数据。WebSockets 是一种提供全双工通信的协议，通常用于实时应用，如聊天、游戏等。

因此，传统的 HTTP 协议是半双工的，而 HTTP/2 和 HTTP/3 通过引入多路复用等技术部分缓解了半双工的限制，但严格来说，HTTP 本身仍然不是完全的全双工协议。

##### http常用状态码集合
以下是 HTTP 状态码的表格分类：

| **类别** | **状态码** | **名称** | **描述** |
| --- | --- | --- | --- |
| **1xx 信息响应** | 100 | Continue | 客户端应继续发送请求的剩余部分。 |
| | 101 | Switching Protocols | 服务器根据客户端请求切换协议。 |
| **2xx 成功响应** | 200 | OK | 请求成功。 |
| | 201 | Created | 请求已成功，并在服务器上创建了新的资源。 |
| | 202 | Accepted | 请求已被接受，但尚未处理。 |
| | 204 | No Content | 请求成功，但没有返回内容。 |
| **3xx 重定向** | 301 | Moved Permanently | 资源已被永久移动到新的 URI。 |
| | 302 | Found | 资源临时被移动到另一个 URI。 |
| | 304 | Not Modified | 资源未被修改，可以使用缓存版本。 |
| **4xx 客户端错误** | 400 | Bad Request | 服务器无法理解请求的语法。 |
| | 401 | Unauthorized | 请求未通过身份验证。 |
| | 403 | Forbidden | 服务器拒绝请求。 |
| | 404 | Not Found | 资源未找到。 |
| | 405 | Method Not Allowed | 请求方法不被允许。 |
| | 408 | Request Timeout | 服务器在等待请求时超时。 |
| **5xx 服务器错误** | 500 | Internal Server Error | 服务器遇到错误，无法完成请求。 |
| | 501 | Not Implemented | 服务器不支持请求所需的功能。 |
| | 502 | Bad Gateway | 服务器作为网关或代理，从上游服务器收到无效响应。 |
| | 503 | Service Unavailable | 服务器当前无法处理请求，通常是暂时的。 |
| | 504 | Gateway Timeout | 服务器作为网关或代理，未能及时从上游服务器接收到响应。 |








