storage

# storage driver
- If aufs is available, default to it
- least amount of configuration is used, such as btrfs or zfs
- overlay2 is preferred, followed by overlay, Neither of these requires extra configuration.
- devicemapper is next, but requires direct-lvm for production environments, because loopback-lvm, while zero-configuration, has very poor performance

## aufs 
- aufs is only supported on Ubuntu and Debian
- operate at the file level rather than the block level

## overlay or overlay2(recommanded)
- disable selinux if you use the overlay or overlay2 driver on CentOS
- For lots of small writes or containers with many layers or deep filesystems, overlay may perform better than overlay2

## devicemapper
- Block-level storage, perform better for write-heavy workloads (though not as well as Docker volumes)

## zfs
- Block-level storage, perform better for write-heavy workloads (though not as well as Docker volumes)
- require a lot of memory
- zfs is a good choice for high-density workloads such as PaaS.

## btrfs
- btrfs is only supported on SLES, which is only supported with Docker EE
- Block-level storage, perform better for write-heavy workloads (though not as well as Docker volumes)
- require a lot of memory


## recommanded
- https://docs.docker.com/engine/userguide/storagedriver/selectadriver/#docker-ce
- https://docs.docker.com/engine/userguide/storagedriver/selectadriver/#supported-backing-filesystems
- When in doubt, the best all-around configuration is to use a modern Linux distribution with a kernel that supports the overlay2 storage driver, and to use Docker volumes for write-heavy workloads instead of relying on writing data to the container’s writable layer
- In general, aufs, overlay, and devicemapper are the choices with the highest stability

## check
- docker info|grep -A4 'Storage Driver'

## jumped
- https://docs.docker.com/engine/userguide/storagedriver/aufs-driver/