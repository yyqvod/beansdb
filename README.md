IIDAD
# What is Beansdb? 

Beansdb is a distributed key-value storage system designed for large scale 
online system, aiming for high avaliablility and easy management. It took 
the ideas from Amazon's Dynamo, then made some simplify to Keep It Simple 
Stupid (KISS). 

The clients write to N Beansdb node, then read from R of them (solving 
conflict). Data in different nodes is synced through hash tree, in cronjob. 
Beansdb base on memcached and Tokyo Cabinet, with efficient persistant 
hash tree (called Hex Tree) support.

It conforms to memcache protocol (not completed, see below), so any memcached 
client can interactive with it without any modification.  

Beansdb is heavy used in http://www.douban.com/, stored images, mp3,  text 
fields and so on, see benchmark below.

Any suggestion or feedback is welcome.


# Features

* High availability data storage with multi readable and writable repications

* Soft state and final consistency, synced with hash tree

* Easy Scaling out without interrupting online service

* High performance read/write for a key-value based object

* Configurable availability/consistency by N,W,R

* Memcache protocol compatibility

## Supported memcache commands

* get
* set(with version support)
* append
* incr
* delete
* stats
* flush_all

## Private commands

* get @xxx, list the content of hash tree, such as @0f
* get ?xxx, get the meta data of key.
