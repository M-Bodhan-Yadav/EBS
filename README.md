# EBS
---
## NAME:  Mellakanti Bodhan Yadav
## REG NO: 212223030021
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

<img width="1873" height="837" alt="Screenshot 2026-08-03 140253" src="https://github.com/user-attachments/assets/bb8ea9c3-15b9-4826-8129-995af9cf5194" />

<img width="1262" height="646" alt="Screenshot 2026-08-20 135512" src="https://github.com/user-attachments/assets/0ddc15ec-d575-4766-9e23-f2399acddead" />

<img width="1478" height="792" alt="Screenshot 2026-08-20 140333" src="https://github.com/user-attachments/assets/d3da2591-31c5-4453-ac89-4c6c715c425a" />




---

### Output 2: EBS Volume Attached to EC2 Instance

The `My Volume` EBS volume is successfully attached to the `Lab` EC2 instance and is in the `In-use` state.

<img width="1476" height="559" alt="Screenshot 2026-08-20 140352" src="https://github.com/user-attachments/assets/8917c81c-c6b9-443f-b6ac-165b3d90b5f5" />

<img width="1480" height="790" alt="Screenshot 2026-08-20 140409" src="https://github.com/user-attachments/assets/343e265b-7a97-4485-97ac-6e4cb58b27e5" />




---

### Output 3: EBS Volume Mounted Successfully

The `df -h` command displays the mounted EBS volume at `/mnt/data-store`.

<img width="1473" height="738" alt="Screenshot 2026-08-20 140422" src="https://github.com/user-attachments/assets/ef2cc468-6765-45cc-acdf-a8e8c63981ef" />


---

### Output 4: File Created and Verified

The file `file.txt` is successfully created inside the EBS volume and the stored text is displayed.

```text
some text has been written
```

<img width="1480" height="786" alt="Screenshot 2026-08-20 140435" src="https://github.com/user-attachments/assets/6fd4bc7a-6f8c-490e-9371-08c6c2ec322e" />



---

### Output 5: EBS Snapshot Created

The AWS EC2 Snapshots page shows `My Snapshot` with the snapshot creation completed successfully.


<img width="1461" height="722" alt="Screenshot 2026-08-20 140448" src="https://github.com/user-attachments/assets/44b49109-f7bb-453f-9117-b240005220b3" />

<img width="1480" height="798" alt="Screenshot 2026-08-20 140500" src="https://github.com/user-attachments/assets/ba51a0bd-6b6e-4ce7-ac9f-0c20ae7493ce" />



---

### Output 6: Snapshot Restored Successfully

The snapshot is restored to a new EBS volume named `Restored Volume`. After attaching and mounting the restored volume, the deleted `file.txt` is successfully recovered.

```text
file.txt
```
<img width="1475" height="579" alt="Screenshot 2026-08-20 140513" src="https://github.com/user-attachments/assets/9f9f73c7-3699-4060-90e5-f2777e93fb18" />

<img width="1474" height="788" alt="Screenshot 2026-08-20 140532" src="https://github.com/user-attachments/assets/c7756e54-ff15-4401-9e41-ed9e8abd663f" />


<img width="1472" height="853" alt="Screenshot 2026-08-20 140552" src="https://github.com/user-attachments/assets/d3bc05c4-6c6b-4cf5-9a8c-1292dc321719" />


<img width="1475" height="583" alt="Screenshot 2026-08-20 140604" src="https://github.com/user-attachments/assets/d08031d3-dae6-4c87-91c1-7a5566ae2c0c" />





---

## Result

Thus, an Amazon EBS volume was successfully created and attached to an Amazon EC2 instance. The volume was formatted with an `ext3` file system, mounted, and used for storing data. An EBS snapshot was successfully created as a backup, and a new EBS volume was restored from the snapshot. The previously deleted `file.txt` was successfully recovered, demonstrating the backup and restore functionality of Amazon EBS.
