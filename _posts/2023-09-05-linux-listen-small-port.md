---
layout: post
title: Linux中监听小端口失败时的排查
date: 2023-09-05
tags: listen port
---
## Linux中监听小端口失败的排查(ubuntu)


1. **系统保护机制** ：某些Linux系统（包括Ubuntu）可能会通过内核参数来限制一些特权端口的使用，以提高系统安全性。你可以尝试通过修改 `/etc/sysctl.conf`文件来放宽这些限制。打开文件并添加以下行来启用低端口（小于1024）的绑定：

<pre><div class="bg-black rounded-md mb-4"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans justify-between rounded-t-md"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4 overflow-y-auto"><code class="!whitespace-pre hljs">net.ipv4.ip_unprivileged_port_start=0
   </code></div></div></pre>

   然后运行以下命令以应用更改：

<pre><div class="bg-black rounded-md mb-4"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans justify-between rounded-t-md"><span>css</span><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4 overflow-y-auto"><code class="!whitespace-pre hljs language-css">sudo sysctl -p
   </code></div></div></pre>

1. **应用程序的配置** ：确保你的应用程序在尝试绑定端口102之前已正确配置。可能存在应用程序配置文件中的问题，导致服务无法正常启动。
2. **其他进程占用端口** ：在某些情况下，其他正在运行的进程可能会占用端口102，即使你已关闭防火墙。请确保没有其他进程正在使用相同的端口。
3. **SELinux或AppArmor** ：Ubuntu系统中可能启用了SELinux或AppArmor，这些安全模块可能会限制进程的网络访问。检查这些模块的配置并根据需要进行调整。
4. **异常情况** ：如果系统出现异常情况，可能导致网络堵塞或其他问题，也会影响绑定端口。在这种情况下，你可能需要重新启动系统或进行故障排除。
