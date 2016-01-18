#### mnawsinaction

cp7 s3
basic commands
```
aws s3 mb s3://name
aws sync localpath s3://name/path
aws cp --recursive s3://name/path localpath
aws s3 rb --force s3://name(may not delete a versioning bucket)
```
Other config
```
aws s3api put-bucket-versioning --bucket bucketname --versioning-configurition Status=Enabled
aws s3api list-object-versions --bucket bucketname
```

cp8 ebs
tweaking performance
```
(testing write)
dd if=/dev/zero of=/mnt/volume/template bs=1M count=1024 conv=fdatasync,notrunc
(testing read)
dd if=/mnt/volume/tempfile of=/dev/null bs=1M count=1024
```

flushing caches(after writing test, do this before doing reading test)
```
echo 3 | tee /proc/sys/vm/drop_caches
```

