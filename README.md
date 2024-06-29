# FSKit Sample

FSKit is the new framework introduced in macOS Sequoia that enables the developer to provide custom filesystem support from user space. The document is almost non-existent at the moment so here is a sample project to show how to use the framework.

`UnaryFilesystemExtension` is the entry point of your custom filesystem. The implementation should return an instance of your custom filesystem implementation.

The filesystem should be a subclass of `FSUnaryFileSystem` and conforms to necessary protocols, specifically `FSBlockDeviceOperations` as the system invokes that when deciding if the custom FS should be used, and `FSUnaryFileSystemOperations` for when the system tries to get a volume out of the resources.

From there, you can create your own subclass of `FSVolume` to help manage your volume and conform to `FSVolumeOperations` to support the basic volume specific operations. For a fully functional volume implementation, you’ll probably need to conform to most of the `FSVolume*Operations`.

Once you build and run the app, you should be able to mount the FS with something like these

```
sudo mkdir /Volumes/TestVol
mount -t MyFS myfs:/a /Volumes/TestVol
```

And unmount them with

```
sudo umount /Volumes/TestVol
```
