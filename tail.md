# Tailing logs

## In Linux

```
tail -n 100 /var/log/my.log
```

* `-n` number of lines to keep in view

## In Windows

In Powershell

```
Get-Content myTestLog.log –Wait
```

eg to tail log for ue project:

```
cd C:\path\to\project\Saved\Logs
Get-Content node_righyt.log –Wait
```
