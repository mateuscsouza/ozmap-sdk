# DIOType Module

This document provides a concise guide to the DIOType module, focusing on the DIOType model and its Data Transfer Objects (DTOs) for creation and update operations.

## Models

### DIOType

Defines the structure for DIO types.

```typescript
type DIOType = {
  id: string;
  code: string;
  brand?: string;
  mold?: string;
  description?: string;
  ratio: number;
  prefix: string;
  size: number;
  loss?: number;
  tray_number: number;
  input_label: string;
  output_label: string;
  external_id?: any;
};
```

### CreateDIOTypeDTO

Defines the structure for creating a DIO type.

```typescript
type CreateDIOTypeDTO = {
  code: string;
  brand?: string;
  mold?: string;
  description?: string;
  ratio: number;
  prefix?: string;
  size?: number;
  loss?: number;
  tray_number: number;
  input_label?: string;
  output_label?: string;
  external_id?: any;
};
```

### UpdateDIOTypeDTO

Defines the structure for updating a DIO type.

```typescript
type UpdateDIOTypeDTO = {
  code?: string;
  brand?: string;
  mold?: string;
  description?: string;
  ratio?: number;
  prefix?: string;
  size?: number;
  loss?: number;
  tray_number?: number;
  input_label?: string;
  output_label?: string;
  external_id?: any;
};
```

## Example Usage

### Creating a DIOType

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateDIOTypeDTO } from './DIOType'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newDIOTypeData = { // CreateDIOTypeDTO type assumed to be available
  code: "DGT-24P",
  ratio: 1, // Assuming 1:1 pass-through or direct termination
  tray_number: 24, // e.g., 24 ports
  input_label: "IN", // Optional in DTO due to .partial, but good to provide
  output_label: "OUT", // Optional in DTO due to .partial, but good to provide
  size: 24, // Optional in DTO (has default), but good to specify
  prefix: "DIO-", // Optional in DTO (has default)
  brand: "Generic", // Optional
  mold: "RackMount-1U", // Optional
  description: "24 Port Rack Mount DIO Type", // Optional
  loss: 0.1, // Optional
  // external_id is optional
};

sdk.dioType.create(newDIOTypeData).then((dioType) => {
  console.log('DIOType created:', dioType);
});
```
Response example:
```json
{
  "_id": "dioTypeIdXYZ",
  "code": "DGT-24P",
  "ratio": 1,
  "tray_number": 24,
  "input_label": "IN",
  "output_label": "OUT",
  "size": 24,
  "prefix": "DIO-",
  "brand": "Generic",
  "mold": "RackMount-1U",
  "description": "24 Port Rack Mount DIO Type",
  "loss": 0.1,
  "external_id": null,
  "createdAt": "2023-10-29T14:00:00.000Z",
  "updatedAt": "2023-10-29T14:00:00.000Z",
  "id": "dioTypeIdXYZ"
}
```

### Updating a DIOType

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateDIOTypeDTO } from './DIOType'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateDIOTypeData = { // UpdateDIOTypeDTO type assumed to be available
  description: "Revised 24 Port Rack Mount DIO Type",
  loss: 0.05, // Improved loss value
};

sdk.dioType.updateById('dioTypeId', updateDIOTypeData).then(() => {
  console.log('DIOType updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetching DIOTypes

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.dioType.find({ page: 1, limit: 10 }).then((pagination) => {
  console.log('DIOTypes:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "dioTypeIdXYZ",
      "code": "DGT-24P",
      "ratio": 1,
      "tray_number": 24,
      "input_label": "IN",
      "output_label": "OUT",
      "size": 24,
      "prefix": "DIO-",
      "brand": "Generic",
      "mold": "RackMount-1U",
      "description": "Revised 24 Port Rack Mount DIO Type",
      "loss": 0.05,
      "external_id": null,
      "createdAt": "2023-10-29T14:00:00.000Z",
      "updatedAt": "2023-10-29T14:05:00.000Z", // Assuming it was updated
      "id": "dioTypeIdXYZ"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a DIOType by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.dioType.findById('dioTypeId').then((dioType) => {
  console.log('DIOType:', dioType);
});
```
Response example:
```json
{
  "_id": "dioTypeIdXYZ",
  "code": "DGT-24P",
  "ratio": 1,
  "tray_number": 24,
  "input_label": "IN",
  "output_label": "OUT",
  "size": 24,
  "prefix": "DIO-",
  "brand": "Generic",
  "mold": "RackMount-1U",
  "description": "Revised 24 Port Rack Mount DIO Type",
  "loss": 0.05,
  "external_id": "ext-dgt-24p-001",
  "createdAt": "2023-10-29T14:00:00.000Z",
  "updatedAt": "2023-10-29T14:05:00.000Z",
  "id": "dioTypeIdXYZ"
}
```

### Deleting a DIOType

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.dioType.deleteById('dioTypeId').then(() => {
  console.log('DIOType deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```

