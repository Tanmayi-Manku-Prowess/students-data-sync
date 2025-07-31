# students-data-sync
This mule application syncs students' records picked from the file of a sftp server, processing every 5 minutes. It syncs the student records to Oracle database and MySql database

## Key Features
- Picks Json file from sftp-root folder from sftp server
- Uses Batch Job to Bulk insert the json data to Oracle database and MySql database within two batch steps.
- On both database success response, routes the file from `/incoming` to `/completed` folder.

## Technologies Used
* MuleSoft Anypoint Studio
* Oracle Database
* MySql Database
* SFTP cloud-based server and WinSCP to manage files remotely.

## Setup references
- SFTP Cloud-based service: https://sftpcloud.io/
- WinSCP (to manage the cloud server): https://winscp.net/eng/download.php#google_vignette
- MySql Database: https://phpmyadmin.freedb.tech/
- Oracle Database

```
CREATE TABLE bulk_students (
    student_id NUMBER PRIMARY KEY,
    student_name VARCHAR2(100),
    student_phone VARCHAR2(15),
    department VARCHAR2(50),
    has_joined VARCHAR2(10)
);
```
## Sample JSON Data

```
[
 {
    "student_id": 101,
    "student_name": "Rakesh Sharma",
    "student_phone": "9000012345",
    "department": "Physics",
    "has_joined": "Yes"
  },
  {
    "student_id": 102,
    "student_name": "Anita Desai",
    "student_phone": "9000012346",
    "department": "Mathematics",
    "has_joined": "No"
  }
]
```
## Students' Inserted into Database Table

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/b001c095-87d7-42c8-be1e-9548f68e50ae" />

## SFTP Cloud server
<img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/131395bf-cb39-417a-bea9-e5c3b36b2f64" />
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/a211c8d5-61e4-4944-a0e8-fabf82cd7d5a" />
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/145a696f-5d1c-47f5-ab44-bdaacbe29de0" />


## Experience Layer Triggerer
<img width="400" height="300" alt="Screenshot 2025-07-31 050456" src="https://github.com/user-attachments/assets/b5b44c9c-235d-4556-829e-aa57762c27e2" />

<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/8d8e76b9-10ee-43b4-8ab6-eabfdbb2b87c" />

## Process Layer Flow with Batch Processor
<img width="2857" height="490" alt="students_omdb_sync_papi" src="https://github.com/user-attachments/assets/03f3819d-0a36-4994-98f3-5cfbef2bafc8" />

## System Layer with Database Insertions and SFTP File picking and routing

### File Picking
<img width="400" height="400" alt="get_get_files_students_omdb_sync_sapi_config" src="https://github.com/user-attachments/assets/f8618768-c64f-43f7-aa68-d64ee0bb1f41" />

### Bulk Insert of records to Oracle Database and MySql Database
<img width="400" height="400" alt="post_mysql_insert_application_json_students_omdb_sync_sapi_config" src="https://github.com/user-attachments/assets/a6177e8a-f856-4cc0-a28f-7e9121743e97" />
<img width="400" height="400" alt="post_oracle_insert_application_json_students_omdb_sync_sapi_config" src="https://github.com/user-attachments/assets/21b32d51-71d9-425e-bbc5-25ea1b8423bc" />

### Routing of processed file to sftp-root folder
<img width="800" height="800" alt="post_route_file_application_json_students_omdb_sync_sapi_config" src="https://github.com/user-attachments/assets/aabc1e8d-a72f-469b-a579-d8965161f16a" />
