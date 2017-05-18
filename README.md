# P2P-Dispatch-Framework（信令服务器）
P2P分发框架－信令服务器，用于控制连接，提供peer端寻找、控制信号转发等功能

端口占用：

        8080:   查看资源情况
        10000:  提供websocket服务


## 一、信令服务器接口
* 3001 操作索引
    * 参数

            {
                code:   3001,
                data:[
                    {
                        url:    "//www.example.com/example",    //资源：url绝对路径（如果客户端没有指定传输协议，则采用通用协议）
                        md5:    "34dfsf3afeefefefe"             //资源：md5校验代码
                    },
                    ...
                ]
            }

    * 返回结果
        * 1001 通知客户端MD5错误，需要丢弃的资源

                {
                    code:   1001,
                    data:[
                        "//www.example.com/example",            //资源：url绝对路径（如果客户端没有指定传输协议，则采用通用协议）
                        ...
                    ]
                }

* 3002 寻找有这些资源的客户端
    * 参数

            {
                code:   3002,
                data:[
                    "//www.example.com/example",                //资源：url绝对路径（如果客户端没有指定传输协议，则采用通用协议）
                    "http://www.example.com/example",
                    "https://www.example.com/example",
                    ...
                ]
            }

    * 返回结果
        * 1002 通知客户端每个的资源的第三方提供者 & 无第三方提供者的资源

            {
                code:   1002,
                data:{

                }
            }

        3001 操作索引
        3002 寻找有这些资源的客户端
        3003 转发提供描述
        3004 转发响应描述
        3005 转发候选信息
        3201 转发数据索取请求

## 二、客户端处理报文

        1001 丢弃资源
        1002 收到可用的客户端
        1003 收到请求描述信息
        1004 收到响应描述
        1005 收到候选信息
        1201 接收到发送数据请求，准备发送数据