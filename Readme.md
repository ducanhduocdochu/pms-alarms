
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
    - [🔍 GET /v1/pms/alarms/folder/unSelected](#-get-v1pmsalarmsfolderunselected) 
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
    "folder": {
        "_id": "673d3b5cef86936629d82ab0",
        "owner": {
            "userId": "66addb4c6e3a159dda2f334a",
            "fullName": "Minh",
            "email": "admin@sametel.com.vn",
            "role": "admin",
            "orgIdName": "vienthong-sametel",
            "_id": "673d3b5cef86936629d82ab1"
        },
        "folderName": "Test ducanh 3",
        "folderNormailizedName": "test ducanh 3",
        "items": [
            "673d3acdef86936629d82a8b",
            "673d3ad1ef86936629d82a94",
            "673d3ad4ef86936629d82a9d"
        ],
        "createdAt": "2024-11-20T01:29:00.477Z",
        "updatedAt": "2024-11-20T01:29:00.477Z",
        "__v": 0
    },
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
                    "_id": "673d3ad4ef86936629d82aa1"
                },
                "lowWarning": {
                    "value": 4,
                    "description": "oh no lowWarning",
                    "_id": "673d3ad4ef86936629d82aa2"
                },
                "highWarning": {
                    "value": 5,
                    "description": "oh no highWarning",
                    "_id": "673d3ad4ef86936629d82aa3"
                },
                "highAlert": {
                    "value": 6,
                    "description": "oh no highWarning",
                    "_id": "673d3ad4ef86936629d82aa4"
                }
            },
            "_id": "673d3ad4ef86936629d82a9d",
            "owner": {
                "userId": "66addb4c6e3a159dda2f334a",
                "fullName": "Minh",
                "email": "admin@sametel.com.vn",
                "role": "admin",
                "orgIdName": "vienthong-sametel",
                "_id": "673d3ad4ef86936629d82a9e"
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
                        "_id": "673d3ad4ef86936629d82aa0"
                    }
                ],
                "interval": 1,
                "intervalType": "minute",
                "dateRange": "today",
                "_id": "673d3ad4ef86936629d82a9f"
            },
            "isOn": true,
            "alarmName": "Test ducanh 6",
            "alarmNormailizedName": "test ducanh 6",
            "dataFormat": "raw",
            "dataType": "accumulated",
            "createdAt": "2024-11-20T01:26:44.515Z",
            "updatedAt": "2024-11-20T01:26:44.515Z",
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
                    "_id": "673d3ad1ef86936629d82a98"
                },
                "lowWarning": {
                    "value": 4,
                    "description": "oh no lowWarning",
                    "_id": "673d3ad1ef86936629d82a99"
                },
                "highWarning": {
                    "value": 5,
                    "description": "oh no highWarning",
                    "_id": "673d3ad1ef86936629d82a9a"
                },
                "highAlert": {
                    "value": 6,
                    "description": "oh no highWarning",
                    "_id": "673d3ad1ef86936629d82a9b"
                }
            },
            "_id": "673d3ad1ef86936629d82a94",
            "owner": {
                "userId": "66addb4c6e3a159dda2f334a",
                "fullName": "Minh",
                "email": "admin@sametel.com.vn",
                "role": "admin",
                "orgIdName": "vienthong-sametel",
                "_id": "673d3ad1ef86936629d82a95"
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
                        "_id": "673d3ad1ef86936629d82a97"
                    }
                ],
                "interval": 1,
                "intervalType": "minute",
                "dateRange": "today",
                "_id": "673d3ad1ef86936629d82a96"
            },
            "isOn": true,
            "alarmName": "Test ducanh 5",
            "alarmNormailizedName": "test ducanh 5",
            "dataFormat": "raw",
            "dataType": "accumulated",
            "createdAt": "2024-11-20T01:26:41.180Z",
            "updatedAt": "2024-11-20T01:26:41.180Z",
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
                    "_id": "673d3acdef86936629d82a8f"
                },
                "lowWarning": {
                    "value": 4,
                    "description": "oh no lowWarning",
                    "_id": "673d3acdef86936629d82a90"
                },
                "highWarning": {
                    "value": 5,
                    "description": "oh no highWarning",
                    "_id": "673d3acdef86936629d82a91"
                },
                "highAlert": {
                    "value": 6,
                    "description": "oh no highWarning",
                    "_id": "673d3acdef86936629d82a92"
                }
            },
            "_id": "673d3acdef86936629d82a8b",
            "owner": {
                "userId": "66addb4c6e3a159dda2f334a",
                "fullName": "Minh",
                "email": "admin@sametel.com.vn",
                "role": "admin",
                "orgIdName": "vienthong-sametel",
                "_id": "673d3acdef86936629d82a8c"
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
                        "_id": "673d3acdef86936629d82a8e"
                    }
                ],
                "interval": 1,
                "intervalType": "minute",
                "dateRange": "today",
                "_id": "673d3acdef86936629d82a8d"
            },
            "isOn": true,
            "alarmName": "Test ducanh 4",
            "alarmNormailizedName": "test ducanh 4",
            "dataFormat": "raw",
            "dataType": "accumulated",
            "createdAt": "2024-11-20T01:26:37.995Z",
            "updatedAt": "2024-11-20T01:26:37.995Z",
            "__v": 0,
            "status": "normal"
        }
    ],
    "total": 3,
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

#### 🔍 GET /v1/pms/alarms/folder/unSelected

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
