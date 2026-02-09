# Offline-AI-Assistant / 离线AI助手

## OpenAI Compatible API Usage Examples / OpenAI 兼容接口调用示例

This project includes a built-in OpenAI compatible HTTP service, with the default endpoint at `http://<device-ip>:8080/v1/chat/completions`. After starting the service, you can use the following examples to make API calls.

本项目内置 OpenAI 兼容的 HTTP 服务，默认端点为 `http://<设备IP>:8080/v1/chat/completions`。服务启动后，可以通过以下示例代码进行调用。

## Usage Examples / 调用示例

### 1. cURL Example (Non-Streaming) / cURL 示例（非流式）
```bash
curl http://<device-ip>:8080/v1/chat/completions \
    -H "Content-Type: application/json" \
    -d '{
        "model": "gemma",
        "messages": [
            {"role": "system", "content": "你是应急救援助手"},
            {"role": "user", "content": "地震后如何判断建筑是否安全？"}
        ]
    }'
```

### 2. cURL Example (Streaming) / cURL 示例（流式）
```bash
curl http://<device-ip>:8080/v1/chat/completions \
    -H "Content-Type: application/json" \
    -d '{
        "model": "gemma",
        "stream": true,
        "messages": [
            {"role": "user", "content": "你好"}
        ]
    }'
```

### 3. OpenAI SDK Example (Node.js) / OpenAI SDK 示例（Node.js）
```javascript
import OpenAI from "openai";

const client = new OpenAI({
    apiKey: "local", // No validation for local service, placeholder only / 本地服务不校验，仅占位
    baseURL: "http://<device-ip>:8080/v1",
});

const completion = await client.chat.completions.create({
    model: "gemma",
    messages: [
        { role: "user", content: "洪水期间如何净化饮用水？" },
    ],
});

console.log(completion.choices[0].message.content);
```

## Notes / 注意事项
- Please replace `<device-ip>` with your actual device IP address / 请将 `<设备IP>` 替换为实际设备的 IP 地址
- The difference between streaming and non-streaming responses is the `stream: true` parameter / 流式响应与非流式响应的区别在于 `stream: true` 参数
- No real API key is needed for local service, any placeholder will work / 本地服务不需要真实的 API key，使用任意占位符即可

## Requirements / 环境要求
- Service is running on the specified port / 服务已启动并运行在指定端口
- Network connection is available / 网络连接正常
- For Node.js example: openai SDK is installed / 对于 Node.js 示例：已安装 openai SDK

---
*Issue created for API usage documentation / 用于 API 使用文档的问题创建*
