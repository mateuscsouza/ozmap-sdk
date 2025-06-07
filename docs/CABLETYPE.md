# CableType Module

This document provides a detailed guide to the CableType module, focusing on the CableType model and its Data Transfer Objects (DTOs) for creation and update operations.

## Models

### CableType

Defines the structure for cable types.

```typescript
type CableType = {
  code: string;
  brand?: string;
  mold?: string;
  default_level: number;
  description?: string;
  config: {
    regular: {
      color: string;
      weight: number;
    };
    not_implanted: {
      color: string;
      weight: number;
    };
  };
  fiberProfile: string;
  fiberNumber: number;
  looseNumber: number;
  base_loss: number;
};
```

### CreateCableTypeDTO

Defines the structure for creating a cable type.

```typescript
type CreateCableTypeDTO = {
  code: string;
  brand?: string;
  mold?: string;
  default_level: number;
  description?: string;
  config: {
    regular: {
      color: string;
      weight: number;
    };
    not_implanted: {
      color: string;
      weight: number;
    };
  };
  fiberProfile: string;
  fiberNumber: number;
  looseNumber: number;
  base_loss: number;
  external_id?: any;
};
```

### UpdateCableTypeDTO

Defines the structure for updating a cable type.

```typescript
type UpdateCableTypeDTO = Partial<CreateCableTypeDTO>;
```

## Example Usage

### Create a CableType

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateCableTypeDTO } from './CableType'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newCableTypeData = { // CreateCableTypeDTO type assumed to be available
  code: 'CT001',
  default_level: 1,
  config: {
    regular: { color: '#3388FFFF', weight: 6 },
    not_implanted: { color: '#FFA500A6', weight: 6 },
  },
  fiberProfile: 'fiberProfileIdValue', // Ensure this ID exists
  fiberNumber: 12,
  looseNumber: 4,
  base_loss: 0.35,
  // brand, mold, description, external_id are optional
};

sdk.cableType.create(newCableTypeData).then((cableType) => {
  console.log('CableType created:', cableType);
});
```
Response example:
```json
{
  "_id": "cableTypeId123",
  "code": "CT001",
  "default_level": 1,
  "config": {
    "regular": { "color": "#3388FFFF", "weight": 6 },
    "not_implanted": { "color": "#FFA500A6", "weight": 6 }
  },
  "fiberProfile": "fiberProfileIdValue",
  "fiberNumber": 12,
  "looseNumber": 4,
  "base_loss": 0.35,
  "brand": null,
  "mold": null,
  "description": null,
  "external_id": null,
  "createdAt": "2023-10-28T14:00:00.000Z",
  "updatedAt": "2023-10-28T14:00:00.000Z",
  "id": "cableTypeId123"
}
```

### Update a CableType

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateCableTypeDTO } from './CableType'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateCableTypeData = { // UpdateCableTypeDTO type assumed to be available
  description: 'Updated description',
};

sdk.cableType.updateById('cableTypeId', updateCableTypeData).then(() => {
  console.log('CableType updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```
### Fetching cableTypes

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.cableType.find().then((pagination) => {
  console.log('cableType:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "cableTypeId123",
      "code": "CT001",
      "default_level": 1,
      "config": {
        "regular": { "color": "#3388FFFF", "weight": 6 },
        "not_implanted": { "color": "#FFA500A6", "weight": 6 }
      },
      "fiberProfile": "fiberProfileIdValue",
      "fiberNumber": 12,
      "looseNumber": 4,
      "base_loss": 0.35,
      "brand": "SuperCables",
      "mold": "SC-MOLD-A",
      "description": "Standard 12-fiber optical cable.",
      "external_id": "ext-ct-001",
      "createdAt": "2023-10-28T14:00:00.000Z",
      "updatedAt": "2023-10-28T14:05:00.000Z",
      "id": "cableTypeId123"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a cableType by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.cableType.findById('cableTypeId').then((cableType) => {
  console.log('cableType:', cableType);
});
```
Response example:
```json
{
  "_id": "cableTypeId123",
  "code": "CT001",
  "default_level": 1,
  "config": {
    "regular": { "color": "#3388FFFF", "weight": 6 },
    "not_implanted": { "color": "#FFA500A6", "weight": 6 }
  },
  "fiberProfile": "fiberProfileIdValue",
  "fiberNumber": 12,
  "looseNumber": 4,
  "base_loss": 0.35,
  "brand": "SuperCables",
  "mold": "SC-MOLD-A",
  "description": "Standard 12-fiber optical cable.",
  "external_id": "ext-ct-001",
  "createdAt": "2023-10-28T14:00:00.000Z",
  "updatedAt": "2023-10-28T14:05:00.000Z",
  "id": "cableTypeId123"
}
```

### Deleting a cableType

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.cableType.deleteById('cableTypeId').then(() => {
  console.log('cableType deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```