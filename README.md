# Note.ms API Usage Guide

由于某些原因，暂时不开放源代码，请使用 demo：[https://notems.dreamqjlight.us.kg](https://notems.dreamqjlight.us.kg)

如何实现此 demo？这是个秘密~

---

## 简介

该服务提供了简单的 API 接口，允许您通过 HTTP 请求与 [Note.ms](https://note.ms) 进行交互。您可以使用 `/write` 接口向指定页面写入文本，或者使用 `/read` 接口从指定页面读取文本。

## 接口说明

### 1. 写入文本到指定页面：`/write`

- **请求方法**：`POST`
- **请求 URL**：`https://notems.dreamqjlight.us.kg/write`
- **请求参数**：

  - `page`（必填）：要写入的页面名称，例如 `0`、`my_page` 等。
  - `text`（必填）：要写入的文本内容。

- **使用示例**：

  ```bash
  curl -X POST 'https://notems.dreamqjlight.us.kg/write' \
    -H 'Content-Type: application/x-www-form-urlencoded' \
    --data-urlencode 'page=0' \
    --data-urlencode 'text=你好，世界！'
  ```

- **成功响应**：

  ```json
  {"status": "success"}
  ```

### 2. 从指定页面读取文本：`/read`

- **请求方法**：`GET`
- **请求 URL**：`https://notems.dreamqjlight.us.kg/read`
- **请求参数**：

  - `page`（必填）：要读取的页面名称，例如 `0`、`my_page` 等。

- **使用示例**：

  ```bash
  curl 'https://notems.dreamqjlight.us.kg/read?page=0'
  ```

- **成功响应**：

  ```json
  {"text": "你好，世界！"}
  ```

## 注意事项

- **速率限制**：每个 IP 对 `/write` 和 `/read` 接口的访问频率限制为每 3 秒一次。如果频繁访问，将返回 `429 Too Many Requests` 错误。

- **字符编码**：请确保在发送和接收文本内容时使用正确的字符编码（UTF-8），以避免出现乱码。

- **错误处理**：如果请求失败，服务器将返回相应的 HTTP 状态码和错误信息。请根据实际情况进行处理。

## 常见问题

### Q1：如何查看我写入的文本是否成功？

使用 `/read` 接口读取指定页面的内容，如果返回的 `text` 与您写入的内容一致，则表示写入成功。

### Q2：为什么我收到 `429 Too Many Requests` 错误？

这是由于您的请求过于频繁。请确保每次请求之间至少间隔 3 秒。

### Q3：我可以写入或读取哪些页面？

您可以自由选择页面名称，但请注意不要与他人发生冲突。常用的页面名称包括数字、字母或它们的组合。

---

感谢您的使用！
