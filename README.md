# 检查一丢丢东西

## 用法

编辑主机和配置文件，运行 `ansible-playbook -uroot -i hosts check.yml`

## 端口检查

编辑 `group_vars/all` 中的 YAML：

~~~yaml
wait_for:
    timeout: 10
    task: local
    ports:
    - 23
    want_state: "stopped"
~~~

### ports

待检测端口列表

### timeout

超时时间，单位是秒

### want_state

- started：端口开放为成功
- stopped：端口关闭为成功

### task

- remote：从指定主机检测远程主机的指定端口
- self：远程主机自行检测 127.0.0.1 的端口
- target：从所有主机检测指定远程主机的指定端口

### remote

任务委托执行主机，仅在 `task` 为 `remote` 和 `target` 时有效。

## modprobe

~~~yaml
modprobe:
    - br_netfilter
~~~

目标系统中必须装载列表中的所有 Mod。

## service

~~~yaml
service:
    - name: "firewalld.service"
      status: "disabled"
      state: "stopped"
~~~

目标主机上，列表中的服务必须是符合此处配置的状态才能够通过检查。

## command

~~~yaml
command:
    - "wget"
    - "ip"
    - "iptables"
    - "ethtool"
    - "socat"
    - "tc"
    - "touch"
~~~

目标主机必须包含列表中指定的所有命令。

## content_denied && content_required

~~~yaml
content_denied:
    - file: "/etc/hosts"
      line: "search"

content_required:
    - file: "/etc/selinux/config"
      line: "SELINUX=enforcing"
~~~

对文本文件进行检查，要求其中必须包含或者不包含某一行内容。