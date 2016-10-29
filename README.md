# RavenDB in Docker container

This container spins up RavenDB single node server instance.

* RavenDB : [official site](https://ravendb.net/)
* Docker: [official site](https://www.docker.com/)
* Windows Containers: [site at MSDN](https://msdn.microsoft.com/virtualization/windowscontainers/containers_welcome)

# Requirements

Windows 2016 build 14393 or Windows 10 build 14393.222 with installed Windows Containers.
To check your OS build, `Win+R` and type `winver`.
At this moment Windows 10 supports Hyper-V Containers only.

To install Windows Containers on your machine follow on of there guides: [Windows Server 2016](https://msdn.microsoft.com/pl-pl/virtualization/windowscontainers/quick_start/quick_start_windows_server), [Windows 10](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/quick_start/quick_start_windows_10)

## Usage
For Windows Server 2016

### Run in background
Run server on port `8080` as service.

```
docker run -d pizycki/ravendb:latest
```

### Run in console and debug mode
Run server on port `8080` in `debug` mode and interactive console.

```
docker run -it -e mode=debug pizycki/ravendb:latest
```

> Running on IIS is not supported here.

### Map storage
Map directory where your databases will be stored to `C:\db\` on your host. You can also map place in your network.
```
docker run -d -v C:\db\:C:\RavenDB\Server\Databases\ pizycki/ravendb:latest 
```

### Map RavenDB listen port
Make you container listen on port `5555`
```
docker run -d -p 5555:8080 pizycki/ravendb:latest 
```

> Both **volume** and **port** mapping work with either `service` and `debug` mode.

---

## Build

Build image with this command

Remember to replace `<tag>` with actual tag, i.e.: RavenDB version.

```
docker build -t pizycki/ravendb:<tag> .
```

# FAQ

## I cannot access my RavenDB server website.
There is something wrong with `localhost`, Win2016 and Docker. I have no idea what can that be.
To get access to RavenDB website, get container IP. Simply type `docker inspect <container_ID>` and look for `Networks.IPAddress`.
Make sure the port you mapped to is open in your firewall settings!