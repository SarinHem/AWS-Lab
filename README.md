# AWS S3 Shell Scripts

This repository contains shell scripts to manage Amazon S3 buckets and objects using AWS CLI.  
Scripts cover bucket creation, deletion, uploading files, listing buckets/objects, syncing files, and backup file renaming.

---

## Prerequisites

- AWS CLI installed and configured (`aws configure`) with appropriate IAM permissions.
- Bash shell environment (Linux, macOS, WSL).
- Network access to AWS.

---

## Script List and Usage

| Script Path              | Description                                        | Usage Example                          |
|-------------------------|--------------------------------------------------|--------------------------------------|
| `./create-bucket`        | Create an S3 bucket (region `ap-southeast-1`)    | `./create-bucket my-unique-bucket`   |
| `./delete-bucket`        | Delete an S3 bucket (use `--force` to empty first) | `./delete-bucket my-bucket --force`  |
| `./put-object`           | Upload a local file to a bucket                   | `./put-object my-bucket ./file.txt`  |
| `./list-bucket`          | List all S3 buckets in your AWS account           | `./list-bucket`                      |
| `./list-object`          | List objects in a bucket, optionally by prefix    | `./list-object my-bucket logs/`      |
| `./sync`                 | Sync local directory to S3 with deletion enabled  | `./sync ./local-dir my-bucket backup/` |
| `./backup/file_got_rename` | Custom script for backup file rename (details depend on your implementation) | `./backup/file_got_rename`            |

---

## Usage Details

### Create Bucket
```bash
./create-bucket <bucket-name>
```

### Delete Bucket
```bash
./delete-bucket <bucket-name> [--force]
```
`--force` empties the bucket before deleting.

### Upload File (Put Object)
```bash
./put-object <bucket-name> <local-file> [s3-key]
```
Uploads file to S3 bucket. If `s3-key` is omitted, filename is used.

### List Buckets
```bash
./list-bucket
```

### List Objects
```bash
./list-object <bucket-name> [prefix]
```

### Sync Directory to S3
```bash
./sync <local-dir> <bucket-name> [s3-prefix]
```
Syncs local folder to bucket and deletes extra files in S3.

### Backup File Rename
```bash
./backup/file_got_rename
```
*Refer to script comments for details.*

---

## Notes

- All scripts assume AWS region `ap-southeast-1` (Singapore). Adjust inside scripts if needed.
- Make sure scripts have execute permission:
  ```bash
  chmod +x ./create-bucket ./delete-bucket ./put-object ./list-bucket ./list-object ./sync ./backup/file_got_rename
  ```
- Ensure your AWS CLI credentials have required permissions.

---

## Troubleshooting

- Test AWS credentials:
  ```bash
  aws sts get-caller-identity
  ```
- Use `--dryrun` option inside sync script if supported for preview.
- Bucket names must be globally unique.

---


