
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
         string,
         string,
          ....
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
            "_id": "673ad9863c68d969d4811466"
        },
        "folderName": "Test ducanh 7",
        "folderNormailizedName": "test ducanh 7",
        "items": [
            "673aaf083793a1f5095426d0",
            "673aaf1a3793a1f5095426d9"
        ],
        "_id": "673ad9863c68d969d4811465",
        "createdAt": "2024-11-18T06:07:02.806Z",
        "updatedAt": "2024-11-18T06:07:02.806Z",
        "__v": 0
    }
}
```

#### ➕ POST /v1/pms/alarms/folder/:folderId

- **Description**: Lấy thông tin folder và các alarm trong folder đó theo `folderId`.

- **Params**:
  `folderId`: id thư mục 

-- **Body**:
```json
{
    "pageNumber": number,
    "pageSize": number, 

    "filter": {
        "dataType": "all", //all or single point or multi point
        "isOn": "all", //on or off or all
        "dataFormat": "all" //raw or option or all
    },
    "sort": {
        "alarmName": "asc", //asc or desc
        "status": "asc", //asc or desc
        "isOn": "asc" //asc or desc
    },
    "search": {
        // "alarmName": "minh3"
    }
}
```

- **Response**:

```json
{
    "items": [
        {
            "activeTime": {
                "hourRange": {
                    "start": {
                        "hour": 7,
                        "minute": 0
                    },
                    "end": {
                        "hour": 17,
                        "minute": 30
                    }
                },
                "dateRange": [
                    1,
                    2,
                    3,
                    4,
                    5,
                    6,
                    7
                ]
            },
            "threshold": {
                "lowAlert": {
                    "value": 3,
                    "description": "oh no lowAlert",
                    "_id": "673aaf1a3793a1f5095426dd"
                },
                "lowWarning": {
                    "value": 4,
                    "description": "oh no lowWarning",
                    "_id": "673aaf1a3793a1f5095426de"
                },
                "highWarning": {
                    "value": 5,
                    "description": "oh no highWarning",
                    "_id": "673aaf1a3793a1f5095426df"
                },
                "highAlert": {
                    "value": 6,
                    "description": "oh no highWarning",
                    "_id": "673aaf1a3793a1f5095426e0"
                }
            },
            "_id": "673aaf1a3793a1f5095426d9",
            "owner": {
                "userId": "66addb4c6e3a159dda2f334a",
                "fullName": "Minh",
                "email": "admin@sametel.com.vn",
                "role": "admin",
                "orgIdName": "vienthong-sametel",
                "_id": "673aaf1a3793a1f5095426da"
            },
            "kpiItem": {
                "displayName": "vol_SN",
                "unit": "kW",
                "formula": null,
                "isRaw": true,
                "isConstant": false,
                "params": [
                    {
                        "name": "vol_SN",
                        "variableName": "",
                        "deviceName": "H 30",
                        "deviceType": "E",
                        "aggregationType": "avg",
                        "_id": "673aaf1a3793a1f5095426dc"
                    }
                ],
                "interval": 1,
                "intervalType": "minute",
                "dateRange": "today",
                "_id": "673aaf1a3793a1f5095426db"
            },
            "isOn": true,
            "alarmName": "Test ducanh 2",
            "alarmNormailizedName": "test ducanh 2",
            "dataFormat": "raw",
            "dataType": "accumulated",
            "createdAt": "2024-11-18T03:06:02.358Z",
            "updatedAt": "2024-11-18T03:06:02.358Z",
            "__v": 0,
            "status": "normal"
        },
        {
            "activeTime": {
                "hourRange": {
                    "start": {
                        "hour": 7,
                        "minute": 0
                    },
                    "end": {
                        "hour": 17,
                        "minute": 30
                    }
                },
                "dateRange": [
                    1,
                    2,
                    3,
                    4,
                    5,
                    6,
                    7
                ]
            },
            "threshold": {
                "lowAlert": {
                    "value": 3,
                    "description": "oh no lowAlert",
                    "_id": "673aaf083793a1f5095426d4"
                },
                "lowWarning": {
                    "value": 4,
                    "description": "oh no lowWarning",
                    "_id": "673aaf083793a1f5095426d5"
                },
                "highWarning": {
                    "value": 5,
                    "description": "oh no highWarning",
                    "_id": "673aaf083793a1f5095426d6"
                },
                "highAlert": {
                    "value": 6,
                    "description": "oh no highWarning",
                    "_id": "673aaf083793a1f5095426d7"
                }
            },
            "_id": "673aaf083793a1f5095426d0",
            "owner": {
                "userId": "66addb4c6e3a159dda2f334a",
                "fullName": "Minh",
                "email": "admin@sametel.com.vn",
                "role": "admin",
                "orgIdName": "vienthong-sametel",
                "_id": "673aaf083793a1f5095426d1"
            },
            "kpiItem": {
                "displayName": "vol_SN",
                "unit": "kW",
                "formula": null,
                "isRaw": true,
                "isConstant": false,
                "params": [
                    {
                        "name": "vol_SN",
                        "variableName": "",
                        "deviceName": "H 30",
                        "deviceType": "E",
                        "aggregationType": "avg",
                        "_id": "673aaf083793a1f5095426d3"
                    }
                ],
                "interval": 1,
                "intervalType": "minute",
                "dateRange": "today",
                "_id": "673aaf083793a1f5095426d2"
            },
            "isOn": true,
            "alarmName": "Test ducanh 1",
            "alarmNormailizedName": "test ducanh 1",
            "dataFormat": "raw",
            "dataType": "accumulated",
            "createdAt": "2024-11-18T03:05:44.955Z",
            "updatedAt": "2024-11-18T03:05:44.955Z",
            "__v": 0,
            "status": "normal"
        }
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
        string,
        string,
        ...
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
