# 端口检测

## 用法

编辑主机和配置文件，运行 `ansible-playbook -uroot -i hosts ping.yml`

## 配置

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

## remote

任务委托执行主机，仅在 `task` 为 `remote` 和 `target` 时有效。
