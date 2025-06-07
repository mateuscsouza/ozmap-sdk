# Building Module

This document provides a concise guide to the Building module, focusing on the Building model and its Data Transfer Objects (DTOs) for creation and update operations.

## Models

### Building

Defines the structure for buildings.

```typescript
// import { BuildingType } from './BuildingType'; // Type is defined globally or not needed for snippet

type Building = {
  kind: 'Building';
  name: string;
  address?: string;
  implanted?: boolean; // default: true
  hasProblem?: boolean; // default: false
  tags?: (string | Tag)[]; // default: []
  project: string | Project;
  cables?: string[]; // default: []
  buildingType: string | BuildingType;
  color?: string;
};
```

### CreateBuildingDTO

Defines the structure for creating a building.

```typescript
type CreateBuildingDTO = {
  name?: string;
  project: string; // Required
  coords: [number, number]; // Required
  pole?: string | null; // Optional
  address?: string;
  implanted?: boolean; // default: true
  tags?: string[]; // default: []
  external_id?: any;
  template?: string;
  buildingType: string; // Required
  color?: string;
  kind?: 'Building'; // Optional, defaults to 'Building' if applicable on backend
};
```

### UpdateBuildingDTO

Defines the structure for updating a building.

```typescript
type UpdateBuildingDTO = {
  name?: string;
  coords?: [number, number]; // Optional
  pole?: string | null; // Optional
  address?: string;
  implanted?: boolean; // default: true
  tags?: string[]; // default: []
  external_id?: any;
  buildingType?: string;
  color?: string;
  // kind is omitted as it's not updatable or derived
};
```

## Example Usage

### Creating a Building

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateBuildingDTO } from './Building'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newBuildingData = { // CreateBuildingDTO type assumed to be available
  name: 'New Building',
  project: 'projectId123', // Added required field
  coords: [-48.5000, -27.6000], // Added required field
  buildingType: 'buildingTypeId',
  implanted: true,
  // kind: 'Building', // Optional, often inferred by the SDK endpoint
  // address, pole, tags, external_id, template, color are optional
};

sdk.building.create(newBuildingData).then((building) => {
  console.log('Building created:', building);
});
```
Response example:
```json
{
  "_id": "buildingId456",
  "name": "New Building",
  "project": "projectId123",
  "coords": [-48.5000, -27.6000],
  "buildingType": "buildingTypeId",
  "implanted": true,
  "kind": "Building",
  "address": null,
  "pole": null,
  "tags": [],
  "cables": [],
  "hasProblem": false,
  "color": null,
  "createdAt": "2023-10-27T10:00:00.000Z",
  "updatedAt": "2023-10-27T10:00:00.000Z",
  "id": "buildingId456"
}
```

### Updating a Building

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateBuildingDTO } from './Building'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateBuildingData = { // UpdateBuildingDTO type assumed to be available
  name: 'Updated Building',
  address: '123 Main St',
};

sdk.building.updateById('buildingId', updateBuildingData).then(() => {
  console.log('Building updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetching Buildings

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.building.find({ page: 1, limit: 10 }).then((pagination) => {
  console.log('Buildings:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "buildingId789",
      "name": "Sample Building",
      "project": "projectId456",
      "coords": [-48.5100, -27.6200],
      "buildingType": "buildingTypeId789",
      "implanted": true,
      "kind": "Building",
      "address": "456 Oak St",
      "pole": null,
      "tags": ["sample-tag"],
      "cables": [],
      "hasProblem": false,
      "color": "blue",
      "createdAt": "2023-10-27T11:00:00.000Z",
      "updatedAt": "2023-10-27T11:05:00.000Z",
      "id": "buildingId789"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a Building by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.building.findById('buildingId').then((building) => {
  console.log('Building:', building);
});
```
Response example:
```json
{
  "_id": "buildingId789",
  "name": "Specific Building",
  "project": "projectId456",
  "coords": [-48.5100, -27.6200],
  "buildingType": "buildingTypeId789",
  "implanted": true,
  "kind": "Building",
  "address": "789 Pine St",
  "pole": "poleIdABC",
  "tags": ["specific-tag", "important"],
  "cables": ["cableId123"],
  "hasProblem": true,
  "color": "red",
  "createdAt": "2023-10-27T12:00:00.000Z",
  "updatedAt": "2023-10-27T12:05:00.000Z",
  "id": "buildingId789"
}
```

### Deleting a Building

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.building.deleteById('buildingId').then(() => {
  console.log('Building deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm deletion, you can ensure the promise resolves successfully, or attempt to fetch the resource again which should result in an error or null.
```
