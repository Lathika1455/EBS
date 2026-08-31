# EBS
## NAME: LATHIKA SREE R
## REG NO: 212224040169
## Aim

To create and configure an Amazon Elastic Block Store (EBS) volume, attach and mount it to an Amazon EC2 instance, create a snapshot backup, and restore the snapshot to a new EBS volume.

---

## Algorithm / Steps

1. Create a new Amazon EBS volume with a size of 1 GiB.
2. Select the same Availability Zone as the EC2 instance.
3. Attach the EBS volume to the EC2 instance using `/dev/sdb`.
4. Connect to the EC2 instance using AWS Systems Manager Session Manager.
5. Check the available storage using `df -h`.
6. Create an `ext3` file system on the EBS volume.
7. Create the `/mnt/data-store` directory.
8. Mount the EBS volume to `/mnt/data-store`.
9. Configure `/etc/fstab` for automatic mounting.
10. Verify that the EBS volume is successfully mounted.
11. Create `file.txt` inside the mounted EBS volume.
12. Verify the contents of the created file.
13. Create an EBS snapshot named `My Snapshot`.
14. Delete `file.txt` from the original EBS volume.
15. Create a new EBS volume from the snapshot.
16. Attach the restored volume to the EC2 instance using `/dev/sdc`.
17. Create the `/mnt/data-store2` directory.
18. Mount the restored volume to `/mnt/data-store2`.
19. Verify that `file.txt` has been successfully restored.

---

## Program

### 1. Check Available Storage

```bash
df -h
```

### 2. Create an ext3 File System

```bash
sudo mkfs -t ext3 /dev/sdb
```

### 3. Create a Mount Directory

```bash
sudo mkdir /mnt/data-store
```

### 4. Mount the EBS Volume

```bash
sudo mount /dev/sdb /mnt/data-store
```

### 5. Configure Automatic Mounting

```bash
echo "/dev/sdb   /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
```

### 6. View the File System Configuration

```bash
cat /etc/fstab
```

### 7. Verify the Mounted Volume

```bash
df -h
```

### 8. Create a File in the EBS Volume

```bash
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
```

### 9. Read the File

```bash
cat /mnt/data-store/file.txt
```

### 10. Delete the File

```bash
sudo rm /mnt/data-store/file.txt
```

### 11. Verify File Deletion

```bash
ls /mnt/data-store/
```

### 12. Create a Mount Directory for the Restored Volume

```bash
sudo mkdir /mnt/data-store2
```

### 13. Mount the Restored EBS Volume

```bash
sudo mount /dev/sdc /mnt/data-store2
```

### 14. Verify Snapshot Restoration

```bash
ls /mnt/data-store2/
```

Expected output:

```text
file.txt
```

---

## Outputs

### Output 1: EBS Volume Created

The AWS EC2 Volumes page shows the newly created `My Volume` EBS volume with a size of 1 GiB.

<img width="1747" height="911" alt="image" src="https://github.com/user-attachments/assets/d8cf6a16-965e-4135-afbc-c28efac20e57" />

<img width="1737" height="900" alt="image" src="https://github.com/user-attachments/assets/471b88da-4de2-4045-bd53-e57815a1bc02" />


---

### Output 2: EBS Volume Attached to EC2 Instance

The `My Volume` EBS volume is successfully attached to the `Lab` EC2 instance and is in the `In-use` state.

<img width="1741" height="897" alt="image" src="https://github.com/user-attachments/assets/13f1018f-911c-4814-a515-cdf4febc1934" />

<img width="1721" height="892" alt="image" src="https://github.com/user-attachments/assets/69fb8151-936b-4288-91ba-85cb8d5fc39d" />

---

### Output 3: EBS Volume Mounted Successfully

The `df -h` command displays the mounted EBS volume at `/mnt/data-store`.

<img width="1900" height="925" alt="image" src="https://github.com/user-attachments/assets/8a7020c7-54f8-4936-82b0-a91583ae9d76" />



---

### Output 4: File Created and Verified

The file `file.txt` is successfully created inside the EBS volume and the stored text is displayed.

```text
some text has been written
```

<img width="1712" height="936" alt="image" src="https://github.com/user-attachments/assets/2a791a88-1cff-4742-a7ad-cc1a4cf96270" />




---

### Output 5: EBS Snapshot Created

The AWS EC2 Snapshots page shows `My Snapshot` with the snapshot creation completed successfully.


<img width="1442" height="711" alt="image" src="https://github.com/user-attachments/assets/a6a2a0bb-cdfd-4e84-bf6f-6e43716fcd84" />

<img width="1436" height="742" alt="image" src="https://github.com/user-attachments/assets/a82dda62-c5c8-43ed-bbe2-d98d3347abfa" />


---

### Output 6: Snapshot Restored Successfully

The snapshot is restored to a new EBS volume named `Restored Volume`. After attaching and mounting the restored volume, the deleted `file.txt` is successfully recovered.

```text
file.txt
```
<img width="1437" height="672" alt="image" src="https://github.com/user-attachments/assets/0845dab7-38e1-4748-882d-11b6a32c378e" />

<img width="1505" height="777" alt="image" src="https://github.com/user-attachments/assets/04e62bd0-37cc-481c-958e-4aa37025c36f" />

<img width="1528" height="540" alt="image" src="https://github.com/user-attachments/assets/25893712-28f3-4b46-bfd2-118d8e6c9316" />


---

## Result

Thus, an Amazon EBS volume was successfully created and attached to an Amazon EC2 instance. The volume was formatted with an `ext3` file system, mounted, and used for storing data. An EBS snapshot was successfully created as a backup, and a new EBS volume was restored from the snapshot. The previously deleted `file.txt` was successfully recovered, demonstrating the backup and restore functionality of Amazon EBS.
