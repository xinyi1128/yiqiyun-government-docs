---
title: "Bucket Notification"
date: 2020-11-25T10:08:56+09:00
description:
collapsible: false
draft: false
weight: 2
---

# DELETE Bucket Notification

删除存储空间的事件通知策略。

获取 Bucket Notification 请参见 [GET Bucket Notification](../get_notification) 。

设置 Bucket Notification 请参见 [PUT Bucket Notification](../put_notification) 。

## Request Syntax

```http
DELETE /?notification HTTP/1.1
Host: <bucket-name>.<zone-id>.obs.yiqiyun.sd.cegn.cn
Date: <date>
Authorization: <authorization-string>
```

## Request Parameters

没有请求参数。

## Request Headers

参见[公共请求头](../../../common_header/#请求头字段-request-header)。

## Request Body

没有请求消息体。

## Response Headers

参见[公共响应头](../../../common_header/#响应头字段-request-header)。

## Example

### Example Request

```http
DELETE /?notification HTTP/1.1
Host: mybucket.zw.obs.yiqiyun.sd.cegn.cn
Date: Sun, 16 Aug 2015 09:05:00 GMT
Authorization: authorization string
```

### Example Response

```http
HTTP/1.1 204 NoContent
Server: QingStor
Date: Sun, 16 Aug 2015 09:05:00 GMT
Content-Length: 0
Connection: close
x-qs-request-id: aa08cf7a43f611e5886952542e6ce14b
```
