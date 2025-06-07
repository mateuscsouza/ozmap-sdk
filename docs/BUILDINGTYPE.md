# BuildingType Module

This document provides a concise guide to the BuildingType module, focusing on the BuildingType model and its Data Transfer Objects (DTOs) for creation and update operations.

## Models

### BuildingType

Defines the structure for building types.

```typescript
type BuildingType = {
  code: string;
  prefix: string;
  default_template?: string;
  description?: string;
  config: {
    implanted: {
      color: string;
    };
    not_implanted: {
      color: string;
    };
  };
};
```

### CreateBuildingTypeDTO

Defines the structure for creating a building type.

```typescript
type CreateBuildingTypeDTO = {
  code: string;
  prefix?: string; // Added
  default_template?: string;
  description?: string;
  config: {
    implanted: {
      color: string;
    };
    not_implanted: {
      color: string;
    };
  };
  external_id?: any;
};
```

### UpdateBuildingTypeDTO

Defines the structure for updating a building type.

```typescript
type UpdateBuildingTypeDTO = {
  code?: string;
  prefix?: string;
  default_template?: string;
  description?: string;
  config?: {
    implanted?: {
      color?: string;
    };
    not_implanted?: {
      color?: string;
    };
  };
  external_id?: any;
};
```

## Example Usage

### Create a BuildingType

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateBuildingTypeDTO } from './BuildingType'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newBuildingTypeData = { // CreateBuildingTypeDTO type assumed to be available
  code: 'Building',
  prefix: 'B-',
  config: {
    implanted: { color: '#3388FFFF' },
    not_implanted: { color: '#FFA500A6' },
  },
  // default_template, description, external_id are optional
};

sdk.buildingType.create(newBuildingTypeData).then((buildingType) => {
  console.log('BuildingType created:', buildingType);
});
```
Response example:
```json
{
  "_id": "buildingTypeId123",
  "code": "Building",
  "prefix": "B-",
  "config": {
    "implanted": { "color": "#3388FFFF" },
    "not_implanted": { "color": "#FFA500A6" }
  },
  "default_template": "defaultTemplateIdIfApplicable",
  "description": null,
  "external_id": null,
  "createdAt": "2023-10-28T10:00:00.000Z",
  "updatedAt": "2023-10-28T10:00:00.000Z",
  "id": "buildingTypeId123"
}
```

### Update a BuildingType

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateBuildingTypeDTO } from './BuildingType'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateBuildingTypeData = { // UpdateBuildingTypeDTO type assumed to be available
  description: 'Updated description',
};

sdk.buildingType.updateById('buildingTypeId', updateBuildingTypeData).then(() => {
  console.log('BuildingType updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetching buildingTypes

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.buildingType.find().then((pagination) => {
  console.log('buildingTypes:', pagination);
});
```

Response example

```json
{
  "total": 0,
  "count": 0,
  "rows": [
    {
      "config": {
        "implanted": {
          "color": "#3388FFFF"
        },
        "not_implanted": {
          "color": "#FFA500A6"
        }
      },
      "description": "Condominio",
      "prefix": "C-",
      "default_template": "5da6146f493d9c00066653f7",
      "createdAt": "2025-04-01T18:09:04.531Z",
      "updatedAt": "2025-04-01T18:09:04.531Z",
      "id": "67ec2bc0a6a57e62760f3225"
    }
  ],
  "start": 0,
  "limit": 0
}
```

### Fetching a buildingType by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.buildingType.findById('buildingTypeId').then((buildingType) => {
  console.log('buildingType:', buildingType);
});
```
Response example:
```json
{
  "_id": "buildingTypeId123",
  "code": "Condo-A",
  "prefix": "CA-",
  "config": {
    "implanted": { "color": "#00FF00" },
    "not_implanted": { "color": "#808080" }
  },
  "default_template": "templateIdXYZ",
  "description": "Condominium Type A",
  "external_id": "ext-condo-a-001",
  "createdAt": "2023-10-28T11:00:00.000Z",
  "updatedAt": "2023-10-28T11:05:00.000Z",
  "id": "buildingTypeId123"
}
```

### Deleting a buildingType

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.buildingType.deleteById('buildingTypeId').then(() => {
  console.log('buildingType deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```
