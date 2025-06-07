# DuctType Module

This document provides a concise guide to the DuctType module, focusing on the DuctType model and its Data Transfer Objects (DTOs) for creation and update operations.

## Models

### DuctType

Defines the structure for duct types.

```typescript
type DuctType = {
  id: string;
  code: string;
  brand?: string;
  mold?: string;
  description?: string;
  subDucts?: SubDuctStructure[];
  config: {
    regular: {
      color: string;
      weight: number;
    };
    notImplanted: {
      color: string;
      weight: number;
    };
  };
  external_id?: any;
};
```

### SubDuctStructure

Defines the structure for sub-ducts within a duct type.

```typescript
type SubDuctStructure = {
  ductType?: string | null;
  color?: string | null;
  subDucts?: SubDuctStructure[] | null;
};
```

### CreateDuctTypeDTO

Defines the structure for creating a duct type.

```typescript
type CreateDuctTypeDTO = {
  code: string;
  brand?: string;
  mold?: string;
  description?: string;
  subDucts?: SubDuctStructure[];
  config?: {
    regular?: {
      color?: string;
      weight?: number;
    };
    notImplanted?: {
      color?: string;
      weight?: number;
    };
  };
  external_id?: any;
};
```

### UpdateDuctTypeDTO

Defines the structure for updating a duct type.

```typescript
type UpdateDuctTypeDTO = {
  code?: string;
  brand?: string;
  mold?: string;
  description?: string;
  subDucts?: SubDuctStructure[];
  config?: {
    regular?: {
      color?: string;
      weight?: number;
    };
    notImplanted?: {
      color?: string;
      weight?: number;
    };
  };
  external_id?: any;
};
```

## Example Usage

### Creating a DuctType

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateDuctTypeDTO } from './DuctType'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newDuctTypeData = { // CreateDuctTypeDTO type assumed to be available
  code: "HDPE-4WAY-RED",
  brand: "DuraLine",
  description: "4-way High-Density Polyethylene duct, red",
  subDucts: [
    { ductType: "subTypeId1", color: "blue" },
    { ductType: "subTypeId1", color: "orange" },
    { ductType: "subTypeId1", color: "green" },
    { ductType: "subTypeId1", color: "brown" }
  ],
  config: { // config is optional in DTO (has default), but can be provided
    regular: { color: "#FF0000", weight: 3 }, // Red
    notImplanted: { color: "#FFA07A", weight: 3 } // Light Salmon for not implanted
  },
  // mold, external_id are optional
};

sdk.ductType.create(newDuctTypeData).then((ductType) => {
  console.log('DuctType created:', ductType);
});
```
Response example:
```json
{
  "_id": "ductTypeId789",
  "code": "HDPE-4WAY-RED",
  "brand": "DuraLine",
  "mold": null,
  "description": "4-way High-Density Polyethylene duct, red",
  "subDucts": [
    { "ductType": "subTypeId1", "color": "blue", "subDucts": null },
    { "ductType": "subTypeId1", "color": "orange", "subDucts": null },
    { "ductType": "subTypeId1", "color": "green", "subDucts": null },
    { "ductType": "subTypeId1", "color": "brown", "subDucts": null }
  ],
  "config": {
    "regular": { "color": "#FF0000", "weight": 3 },
    "notImplanted": { "color": "#FFA07A", "weight": 3 }
  },
  "external_id": null,
  "createdAt": "2023-10-30T11:00:00.000Z",
  "updatedAt": "2023-10-30T11:00:00.000Z",
  "id": "ductTypeId789"
}
```

### Updating a DuctType

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateDuctTypeDTO } from './DuctType'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateDuctTypeData = { // UpdateDuctTypeDTO type assumed to be available
  brand: "DuraLine (Revised)",
  description: "4-way HDPE duct, red, revised specification",
  config: {
    regular: { color: "#E30000", weight: 3 }, // Darker Red
    notImplanted: { color: "#FF8C69", weight: 3 }
  }
};

sdk.ductType.updateById('ductTypeId', updateDuctTypeData).then(() => {
  console.log('DuctType updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetching DuctTypes

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.ductType.find({ page: 1, limit: 10 }).then((pagination) => {
  console.log('DuctTypes:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "ductTypeId789",
      "code": "HDPE-4WAY-RED",
      "brand": "DuraLine (Revised)",
      "mold": null,
      "description": "4-way HDPE duct, red, revised specification",
      "subDucts": [
        { "ductType": "subTypeId1", "color": "blue", "subDucts": null },
        { "ductType": "subTypeId1", "color": "orange", "subDucts": null },
        { "ductType": "subTypeId1", "color": "green", "subDucts": null },
        { "ductType": "subTypeId1", "color": "brown", "subDucts": null }
      ],
      "config": {
        "regular": { "color": "#E30000", "weight": 3 },
        "notImplanted": { "color": "#FF8C69", "weight": 3 }
      },
      "external_id": null,
      "createdAt": "2023-10-30T11:00:00.000Z",
      "updatedAt": "2023-10-30T11:05:00.000Z", // Assuming updated
      "id": "ductTypeId789"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a DuctType by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.ductType.findById('ductTypeId').then((ductType) => {
  console.log('DuctType:', ductType);
});
```
Response example:
```json
{
  "_id": "ductTypeId789",
  "code": "HDPE-4WAY-RED",
  "brand": "DuraLine (Revised)",
  "mold": "MOLD-XYZ", // Example value
  "description": "4-way HDPE duct, red, revised specification",
  "subDucts": [
    { "ductType": "subTypeId1", "color": "blue", "subDucts": null },
    { "ductType": "subTypeId1", "color": "orange", "subDucts": null },
    { "ductType": "subTypeId1", "color": "green", "subDucts": null },
    { "ductType": "subTypeId1", "color": "brown", "subDucts": null }
  ],
  "config": {
    "regular": { "color": "#E30000", "weight": 3 },
    "notImplanted": { "color": "#FF8C69", "weight": 3 }
  },
  "external_id": "ext-dt-002",
  "createdAt": "2023-10-30T11:00:00.000Z",
  "updatedAt": "2023-10-30T11:05:00.000Z",
  "id": "ductTypeId789"
}
```

### Deleting a DuctType

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.ductType.deleteById('ductTypeId').then(() => {
  console.log('DuctType deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```