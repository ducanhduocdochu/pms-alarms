
# 📊 Folder Management System Documentation

## 📑 Mục lục
- [📂 Schemas](#schemas)
  - [📄 Folder Schema](#folder-schema)
- [📝 API Documentation](#api-documentation)
  - [📊 Folder API](#folder-api)
    - [➕ POST /v1/pms/alarms/folder](#-post-v1pmsalarmsfolder)  
    - [➕ POST /v1/pms/alarms/folder/:folderId](#-post-v1pmsalarmsfolderfolderid)  
    - [✏️ PUT /v1/pms/alarms/folder/:folderId](#️-put-v1pmsalarmsfolderfolderid)  
    - [🗑️ DELETE /v1/pms/alarms/folder/:folderId](#️-delete-v1pmsalarmsfolderfolderid)  
    - [🔍 GET /v1/pms/alarms/folder](#-get-v1pmsalarmsfolder)
    - [🔍 GET /v1/pms/alarms/folder/unSelect](#-get-v1pmsalarmsfolderunselect) 
---

## Schemas

### Folder Schema

- **Mô tả**: Lưu trữ thông tin folder

```javascript
const folderSchema = new Schema(
    {
      owner: {
        type: {
          userId: { type: String, required: true },
          fullName: { type: String, required: true },
          email: { type: String, required: true },
          role: {
            type: String,
            required: true,
            enum: ["admin", "member"],
            default: "member",
          },
          orgIdName: { type: String, required: true },
        },
      },
      folderName: {
        type: String,
        required: true,
        trim: true,
      },
      folderNormailizedName: {
        type: String,
        required: true,
        trim: true,
      },
      items: {
        type: [String], 
        required: true,
      },
    },
    { timestamps: true }
  );
```

---

## API Documentation

> Note: Tất cả các api cần header: { 'platform' : 'pms'} và cookies: { 'pms' : 'replaceCookie' }

### Folder API

#### ➕ POST /v1/pms/alarms/folder

- **Description**: Tạo một folder mới cho báo cáo cùng các alarm muốn cho vào.

- **Body**:

```json
{
    "folderName": string, 
    "items": [
        {
            "_id": string,
            "alarmName": string
        },
        {
            "_id":  string,
            "alarmName":  string
        }
    ]
}
```

- **Response**: (case success)

```json
{
    "message_en": "Folder created successfully",
    "message_vn": "Tạo thư mục thành công",
    "item": {
        "owner": {
            "userId": "66addb4c6e3a159dda2f334a",
            "fullName": "Minh",
            "email": "admin@sametel.com.vn",
            "role": "admin",
            "orgIdName": "vienthong-sametel",
            "_id": "673d5bb568baffa9a5b793c0"
        },
        "folderName": "Test ducanh 4",
        "folderNormailizedName": "test ducanh 4",
        "items": [
            {
                "_id": "673d51b89746e6a3e8e61fc7",
                "alarmName": "Test ducanh 2"
            },
            {
                "_id": "673d51b49746e6a3e8e61fbe",
                "alarmName": "Test ducanh 1"
            }
        ],
        "_id": "673d5bb568baffa9a5b793bf",
        "createdAt": "2024-11-20T03:47:02.000Z",
        "updatedAt": "2024-11-20T03:47:02.000Z",
        "__v": 0
    }
}
```

#### ➕ POST /v1/pms/alarms/folder/:folderId

- **Description**: Lấy thông tin folder và các alarm trong folder đó theo `folderId`.

- **Params**:
  `folderId`: id thư mục 

- **Response**:

```json
{
    "folder": {
        "_id": "673d51e69746e6a3e8e61fd0",
        "owner": {
            "userId": "66addb4c6e3a159dda2f334a",
            "fullName": "Minh",
            "email": "admin@sametel.com.vn",
            "role": "admin",
            "orgIdName": "vienthong-sametel",
            "_id": "673d51e69746e6a3e8e61fd1"
        },
        "folderName": "Test ducanh 4",
        "folderNormailizedName": "test ducanh 4",
        "items": [
            "673d51b49746e6a3e8e61fbe",
            "673d51b89746e6a3e8e61fc7"
        ],
        "createdAt": "2024-11-20T03:05:10.492Z",
        "updatedAt": "2024-11-20T03:05:10.492Z",
        "__v": 0
    },
    "items": [
        "673d51b89746e6a3e8e61fc7",
        "673d51b49746e6a3e8e61fbe"
    ],
    "total": 2,
    "page": 1,
    "pageSize": 5
}
```

#### ✏️ PUT /v1/pms/alarms/folder/:folderId 

- **Description**: Cập nhật thông tin folder, có thêm đổi tên hay thêm alarms

- **Params**:
  `folderId`: id folder

- **Body**:

```json
{
    "folderName": string, 
    "items": [
        {
            "_id": string,
            "alarmName": string
        },
        {
            "_id":  string,
            "alarmName":  string
        }
    ]
}
```

- **Response**:

```json
{
    "message_en": "Folder updated successfully",
    "message_vn": "Cập nhật thư mục thành công",
    "item": {
        "_id": "673ad9863c68d969d4811465",
        "owner": {
            "userId": "66addb4c6e3a159dda2f334a",
            "fullName": "Minh",
            "email": "admin@sametel.com.vn",
            "role": "admin",
            "orgIdName": "vienthong-sametel",
            "_id": "673ad9863c68d969d4811466"
        },
        "folderName": "Test ducanh 2",
        "folderNormailizedName": "test ducanh 2",
        "items": [
            "ducanh1",
            "ducanh2",
            "ducanh3"
        ],
        "createdAt": "2024-11-18T06:07:02.806Z",
        "updatedAt": "2024-11-18T06:10:13.431Z",
        "__v": 0
    }
}
```

#### 🗑️ DELETE /v1/pms/alarms/folder/:folderId

- **Description**: Xóa folder theo `folderId`.

- **Params**:
  `reportId`: id báo cáo

- **Response**:

```json
{
    "message_en": "Folder deleted successfully",
    "message_vn": "Xóa thư mục thành công",
    "item": {
        "_id": "673ad9863c68d969d4811465",
        "owner": {
            "userId": "66addb4c6e3a159dda2f334a",
            "fullName": "Minh",
            "email": "admin@sametel.com.vn",
            "role": "admin",
            "orgIdName": "vienthong-sametel",
            "_id": "673ad9863c68d969d4811466"
        },
        "folderName": "Test ducanh 2",
        "folderNormailizedName": "test ducanh 2",
        "items": [
            "ducanh1",
            "ducanh2",
            "ducanh3"
        ],
        "createdAt": "2024-11-18T06:07:02.806Z",
        "updatedAt": "2024-11-18T06:10:13.431Z",
        "__v": 0
    }
}
```

#### 🔍 GET /v1/pms/alarms/folder

- **Description**: Lấy danh sách các folder

- **Query**:
  `pageNumber`: số trang
  `pageSize`: số alarm mỗi trang
  `sortByName`: sắp xếp theo tên
  `searchByName`: tìm kiếm theo tên

- **Response**:

```json
{
    "message_en": "Get list folder successfully",
    "message_vn": "Lấy danh sách folder thành công",
    "items": [
        {
            "_id": "673a9759a761c01db63e9e29",
            "owner": {
                "userId": "66addb4c6e3a159dda2f334a",
                "fullName": "Minh",
                "email": "admin@sametel.com.vn",
                "role": "admin",
                "orgIdName": "vienthong-sametel",
                "_id": "673a9759a761c01db63e9e2a"
            },
            "folderName": "Test ducanh 5",
            "folderNormailizedName": "test ducanh 5",
            "items": [
                "ducanh1",
                "ducanh2"
            ],
            "createdAt": "2024-11-18T01:24:41.136Z",
            "updatedAt": "2024-11-18T01:24:41.136Z",
            "__v": 0
        }
    ],
    "total": 1,
    "page": 1,
    "pageSize": 5
}
```

#### 🔍 GET /v1/pms/alarms/folder/unSelect

- **Description**: Lấy danh sách các alarm chưa được cho vào folder

- **Response**:

```json
{
    "message_en": "Get alarms unselected successfully",
    "message_vn": "Lấy danh sách cảnh báo không được chọn thành công",
    "items": [
        {
            "_id": "673d3c09c28f81b1bd4a8522",
            "alarmName": "Test ducanh 7"
        },
        {
            "_id": "673d3c0cc28f81b1bd4a852b",
            "alarmName": "Test ducanh 8"
        }
    ]
}
```
