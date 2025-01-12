# 调用 gpt-3.5-turbo

## 举个栗子

```
import openai

openai.api_key="OpenAI api key"
messages = []
system_message = input("What type of chatbot you want me to be?")
system_message_dict = {
    "role": "system",
    "content": system_message
}
messages.append(system_message_dict)
message = input("输入想要询问的信息: ")
user_message_dict = {
    "role": "user",
    "content": message
}
messages.append(user_message_dict)
response=openai.chat.Completion.create(
  model="gpt-3.5-turbo",
  messages=messages
)
print(response)
reply = response["choices"][0]["message"]["content"]
print(reply)
```

详细说明:

`openai.chat.Completion.create` 函数内包括了以下几个参数, 这些参数是一个 JSON 字典

1. **model**. 指定模型类别, 如 gpt-3.5-turbo-0125
2. **messages**. 必需, 包含从头到尾的对话历史
   1. **System message**. 一个 json 对象, 包括 content 和 role. content 表示 system 的消息内容; role 表示发出消息的角色, 对 system message 应为 "system"
   2. **User message**. 包含 content 和 role. content 为 string 时表示消息的文本内容, 为 array 时表示发出消息的角色; role 应为 "user"
   3. **Assistant message**. 包括 content, role, name, tool_calls, function_call. role 应为 "assistant"
   4. Tool message. 一个 json 对象, 用户根据 assistant 的 tool_calls 调用某函数后, 用户需要将函数调用结果反馈给大模型, 让大模型给出最终的总结性答复
   5. Function message. 已弃用, 一些旧代码里可能有
3. **tools**
4. **tool_choice**
5. **stream**
6. 