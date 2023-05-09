---
title: Nginx的负载均衡策略
date: 2023-05-08 22:13:50
category: nginx
uri: nginx-load-balancing
tags: 
    - nginx
    - 负载均衡
---
Nginx 支持多种负载均衡策略，可以根据不同的需求选择合适的策略。以下是一些常见的负载均衡策略：

## 轮询（Round Robin）
轮询是 Nginx 默认的负载均衡策略。当有多个后端服务器时，Nginx 会按照顺序将请求分发给每个服务器，每个服务器处理的请求数大致相同。这种策略适用于所有服务器的处理能力相同的情况。

```nginx
upstream backend {
    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com;
}
```
这个配置将使用轮询策略将请求分配给三个后端服务器，每个服务器处理的请求数大致相同。

## IP 哈希（IP Hash）
IP 哈希策略将客户端的 IP 地址计算成一个哈希值，并将哈希值与后端服务器的 IP 地址进行比较，然后将请求发送到与哈希值匹配的服务器上。这种策略可以确保同一个客户端的请求始终发送到同一个服务器上，可以有效避免一些会话相关的问题。

```nginx
upstream backend {
    ip_hash;
    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com;
}
```
这个配置将使用 IP 哈希策略将请求发送到匹配的服务器上，可以确保同一个客户端的请求始终发送到同一个服务器上。

## 最少连接（Least Connections）
最少连接策略将请求发送到当前连接数最少的服务器上。这种策略适用于服务器的处理能力不相同的情况，可以让处理能力较强的服务器处理更多的请求，从而提高系统的整体性能。
```nginx
upstream backend {
    least_conn;
    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com;
}
```
这个配置将使用最少连接策略将请求发送到当前连接数最少的服务器上，可以让处理能力较强的服务器处理更多的请求。


## 加权轮询（Weighted Round Robin）
加权轮询策略将请求按照权重分配给不同的服务器。每个服务器的权重越高，则每次处理请求的次数越多。这种策略适用于服务器的处理能力不同，可以根据服务器的处理能力分配不同的权重，让处理能力较强的服务器处理更多的请求。
```nginx
upstream backend {
    server backend1.example.com weight=3;
    server backend2.example.com weight=2;
    server backend3.example.com weight=1;
}
```
这个配置将使用加权轮询策略将请求按照权重分配给不同的服务器，权重越高的服务器处理请求的次数越多。

## 加权最少连接（Weighted Least Connections）
加权最少连接策略结合了加权轮询和最少连接两种策略的特点，将请求分配给当前连接数最少的服务器上，并考虑每个服务器的权重。这种策略可以在服务器的处理能力不同的情况下，确保每个服务器的负载相对平衡。
```nginx
upstream backend {
    least_conn;
    server backend1.example.com weight=3;
    server backend2.example.com weight=2;
    server backend3.example.com weight=1;
}
```
这个配置将使用加权最少连接策略将请求分配给当前连接数最少的服务器上，并考虑每个服务器的权重，可以确保每个服务器的负载相对平衡。