# cfnat

Cloudflare NAT 优选工具，自动扫描 CF IP 并转发流量到最优节点。

## 功能

- 自动扫描 Cloudflare 有效 IP
- 按延迟排序，优选最优节点
- 支持 IPv4 / IPv6
- 支持数据中心筛选
- 多 IP 负载均衡
- 自动故障切换

## 下载

从 [Releases](https://github.com/issakk/cfnat/releases) 下载对应平台的二进制文件。

## 使用

```bash
# 基本用法
./cfnat -addr 0.0.0.0:1234 -port 443

# 筛选数据中心
./cfnat -colo HKG,SJC,LAX

# IPv6 模式
./cfnat -ips 6

# 自定义参数
./cfnat -addr 0.0.0.0:8080 -port 443 -delay 500 -ipnum 30 -num 5 -task 200
```

## 参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `-addr` | `0.0.0.0:1234` | 本地监听地址 |
| `-port` | `443` | 转发目标端口 |
| `-code` | `200` | 期望的 HTTP 状态码 |
| `-colo` | | 数据中心筛选（逗号分隔） |
| `-delay` | `300` | 有效延迟阈值（毫秒） |
| `-domain` | `cloudflaremirrors.com/debian` | 状态码检查域名 |
| `-ipnum` | `20` | 提取的有效 IP 数量 |
| `-ips` | `4` | IP 类型：`4` 或 `6` |
| `-num` | `5` | 目标负载 IP 数量 |
| `-task` | `100` | 并发协程数 |
| `-tls` | `true` | 是否 TLS 端口 |
| `-random` | `true` | 随机生成 IP |

## 构建

```bash
go build -ldflags="-s -w" -o cfnat .
```
