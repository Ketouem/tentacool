# tentacool
[![Gobuild Download](https://img.shields.io/badge/gobuild-download-green.svg?style=flat)](http://gobuild.io/github.com/optiflows/tentacool)
[![Go Walker](https://img.shields.io/badge/GoWalker-Doc-blue.svg?style=flat)](https://gowalker.org/github.com/optiflows/tentacool)
[![Travis](https://travis-ci.org/Ketouem/tentacool.svg?branch=master)](https://travis-ci.org/Ketouem/tentacool)
[![Drone.io](https://drone.io/github.com/Ketouem/tentacool/status.png)](https://drone.io/github.com/Ketouem/tentacool/latest)
## Description

`tentacool` is a Go server controlled via RESTful API through a Unix Domain Socket.

## Goal

Main goal is to manage all under the hood services for a simple "box".
All done with a auditable, fast and bulletproof software.

So many software do frontend, backend and system... And finally run in `root` by easiness.

## To build

Be sure to set the correct GOPATH and GOROOT environment variables.
You can make use of [godeb](https://github.com/niemeyer/godeb) which set you up with the version of Go you want. (Tentacool is using >= 1.2)

Build Tentacool with [gom](https://github.com/mattn/gom) or [gopm](https://github.com/gpmgo/gopm) with the given `Gomfile` and `.gopmfile`.

### Example with `gom`

```
go get github.com/mattn/gom
gom install
gom build
./tentacool -help
```

## API

### addresses

#### <a name="address"></a>address object

* `link`: interface to manage
* `ip`: ip to add ([CIDR](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) format)
* `id`

#### `GET /addresses`

List all current addresses

##### Response

* Array
  * [address](#address)


#### `GET /addresses/:id`

##### Response

* [address](#address)

#### `POST /addresses`

Add a new address to manage.

##### parameters

* [address](#address)
`id` optional

##### Response

* [address](#address)
* headers
  * `X-Error`: if address is stored in BD but fail to by apply.

##### Example

* without id
```json
==>
{
  "link":"eth0",
  "ip":"192.168.32.11/32",
}
```
```json
<==
{
  "id":"1",
  "link":"eth0",
  "ip":"192.168.32.11/32",
}
```
* with id
```json
==>
{
  "id":"foo",
  "link":"eth0",
  "ip":"192.168.32.12/32",
}
```
```json
<==
{
  "id":"foo",
  "link":"eth0",
  "ip":"192.168.32.12/32",
}
```

#### `PUT /addresses/:id`

Modify an existing address

##### parameters

* [address](#address)
`id` ignored

##### Response

* [address](#address)
* headers
  * `X-Error`: if address is stored in BD but fail to by apply.
