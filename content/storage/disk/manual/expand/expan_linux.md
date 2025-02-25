---
title: "扩容 Linux 数据盘"
date: 2020-01-30T00:38:25+09:00
description: Test description
draft: false
enableToc: false
weight: 20
keyword: 山河
---

## 扩展云硬盘容量

1. 登录到云服务器，执行 `umount` 命令将挂载的目录卸载，然后登录到控制台，将主机与硬盘解除绑定，直至硬盘状态为可用。


2. 在硬盘列表右键点击需要扩容的硬盘，选择**扩容**，弹出**扩容硬盘**界面。

  ![扩容硬盘](/storage/disk/quickstart/_images/expan_linux_1_gov.png)
  
3. 拖动容量滑块或直接输入容量值，点击**提交**即可。

4. 将硬盘重新加载到云服务器。


##  扩展EXT 文件系统

### 扩展无分区磁盘 (ext)

1. 执行`df -h`查看扩容前的磁盘容量。

   ![expan_linux_2](/storage/disk/quickstart/_images/image-1568775109191.png)

2. 查看磁盘文件系统类型。

   ![expan_linux_3](/storage/disk/quickstart/_images/image-1568775112136.png)

3. 使用 `umount` 命令将扩容的磁盘从系统的目录卸载。

4. 执行以下命令，检查扩容后的分区。

   ![expan_linux_4](/storage/disk/quickstart/_images/image-1568775116295.png)

5. 执行 `resize2fs` 命令扩容文件系统。

   ![expan_linux_5](/storage/disk/quickstart/_images/image-1568775120838.png)

6. 使用 `mount` 命令将扩容后的磁盘挂载到系统目录，并检查容量变化。

   ![expan_linux_6](/storage/disk/quickstart/_images/image-1568775127021.png)

###  扩容磁盘原有分区 (ext)

1. 查看扩容前的磁盘容量。

   ![expan_linux_7](/storage/disk/quickstart/_images/image-1568775131616.png)

2. 使用 `umount` 命令将扩容的磁盘从系统的目录卸载。

3. 使用 parted 工具查看磁盘分区的信息。

   ![expan_linux_8](/storage/disk/quickstart/_images/image-1568775135401.png)

4. 输入 `unit s` ，按 `Enter` ，设置磁盘的计量单位为磁柱。

5. 输入 `p`，并回车，查看并记录分区的 Start 值。

   > **注意**：删除分区并新建后，Start 值必须保持不变，否则将会引起数据丢失。

   ![expan_linux_9](/storage/disk/quickstart/_images/image-1568775141798.png)

6. 执行以下命令，删除原有分区。

   ![expan_linux_10](/storage/disk/quickstart/_images/image-1568775146683.png)

7. 执行以下命令，新建一个主分区，Start 值与原来一致，结束值 100%。

   `mkpart primary 63s 100%`

   如果出现如下图所示的状态，请输入 `Ignore`.

   ![expan_linux_11](/storage/disk/quickstart/_images/image-1568775150955.png)

8. 输入 `p` 查看现有分区信息。

   ![expan_linux_12](/storage/disk/quickstart/_images/image-1568775153978.png)

9. 输入 `q` 退出 parted 分区工具。

10. 执行 `partprobe` 命令将分区表同步至文件系统。

11. 执行以下命令，检查扩容后的分区。

    ![expan_linux_13](/storage/disk/quickstart/_images/image-1568775166562.png)

12. 执行 `resize2fs` 命令扩容文件系统。

    ![expan_linux_14](/storage/disk/quickstart/_images/image-1568775181049.png)

13. 使用 `mount` 命令将扩容后的磁盘挂载到系统目录，并检查容量变化。

    ![expan_linux_15](/storage/disk/quickstart/_images/image-1568775184210.png)

##  扩展XFS 文件系统

### 扩展无分区磁盘 (xfs)

1. 执行`df -h`查看扩容前的磁盘容量。

   ![expan_linux_16](/storage/disk/quickstart/_images/fnLwIaSkDeorbjtM.png)

2. 使用 `umount` 命令将扩容的磁盘从系统的目录卸载。

3. 执行以下命令，检查扩容后的分区。

   ![expan_linux_17](/storage/disk/quickstart/_images/image-1568775189304.png)
   输入结果为 0，说明正常

4. 使用 `mount` 命令将扩容后的磁盘挂载到系统目录。

5. 使用 `xfs_growfs` 命令扩容。

   ![expan_linux_18](/storage/disk/quickstart/_images/image-1568775190952.png)

6. 检查扩容后的容量。

   ![expan_linux_19](/storage/disk/quickstart/_images/image-1568775196249.png)

### 扩展磁盘原有分区 (xfs)

1. 查看扩容前的磁盘容量。

   ![expan_linux_20](/storage/disk/quickstart/_images/image-1568775199434.png)

2. 使用 `umount` 命令将扩容的磁盘从系统的目录卸载。

3. 使用 `parted` 工具查看磁盘分区的信息。

   ![expan_linux_21](/storage/disk/quickstart/_images/image-1568775201575.png)

4. 输入 `unit s`，按 `Enter`，设置磁盘的计量单位为磁柱。

5. 输入 `p`，并回车，查看并记录分区的 Start 值。

   > **注意**：删除分区并新建后，Start 值必须保持不变，否则将会引起数据丢失。

   ![expan_linux_22](/storage/disk/quickstart/_images/image-1568775203109.png)

6. 执行以下命令，删除原有分区。

   ![expan_linux_23](/storage/disk/quickstart/_images/image-1568775204602.png)

7. 执行以下命令，新建一个主分区，Start 值与原来一致，结束值 100%。

   ```
   mkpart primary 63s 100%
   ```

   如果出现如下图所示的状态，请输入 `Ignore`。

   ![expan_linux_24](/storage/disk/quickstart/_images/image-1568775206304.png)

8. 输入 `p` 查看现有分区信息。

   ![expan_linux_25](/storage/disk/quickstart/_images/image-1568775207418.png)

9. 输入 `q` 退出 parted 分区工具。

10. 执行 `partprobe` 命令将分区表同步至文件系统。

11. 执行以下命令，检查扩容后的分区。

    ![expan_linux_26](/storage/disk/quickstart/_images/image-1568775209585.png)

12. 执行 `mount` 命令将分区挂载到系统目录。

    ```
    mount /dev/sdb1 /opt
    ```

13. 执行 `xfs_growfs` 命令扩容文件系统。

    ![expan_linux_27](/storage/disk/quickstart/_images/image-1568775211498.png)

14. 使用 `df` 命令检查容量变化。

    ![expan_linux_28](/storage/disk/quickstart/_images/image-1568775213026.png)
