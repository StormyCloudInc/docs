# Grow Disk Size

1.  **Install `parted`**: If it's not already installed, use:

    Copy

    ```
    sudo apt update
    sudo apt install parted
    ```
2.  **Resize the Partition with `parted`**:

    &#x20;

    Start `parted` on the disk:

    Copy

    ```
    sudo parted /dev/sda
    ```

    In the `parted` prompt, resize the partition:

    Copy

    ```
    (parted) print
    (parted) resizepart 3 100%
    ```

    This command resizes partition 3 to use 100% of the available space.
3.  **Resize the Physical Volume**:

    Copy

    ```
    sudo pvresize /dev/sda3
    ```
4.  **Extend the Logical Volume**:

    Copy

    ```
    sudo lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
    ```
5.  **Resize the Filesystem**:

    Copy

    ```
    sudo resize2fs /dev/ubuntu-vg/ubuntu-lv
    ```
