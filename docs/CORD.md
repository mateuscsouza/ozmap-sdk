# Cord Module

This document provides a concise guide to the Cord module, focusing on the Cord model and its Data Transfer Objects (DTOs) for creation and update operations.

## Models

### Cord

Defines the structure for cords.

```typescript
type Cord = {
  _id: string;
  id: string;
  kind: "CORD";
  name?: string; // Added
  parent: string; // Simplified type, ID of the BaseBox
  project: string; // Added, ID of the Project
  connectors: string[]; // Added, Array of Connector IDs
  external_id?: any;
  createdAt: string | Date; // Added from BaseModel
  updatedAt: string | Date; // Added from BaseModel
};
```

### CreateCordDTO

Defines the structure for creating a cord.

```typescript
type CreateCordDTO = {
  parent: string; // ID of the BaseBox
  name?: string; // Added
  external_id?: any;
};
```

### UpdateCordDTO

Defines the structure for updating a cord.

```typescript
type UpdateCordDTO = {
  name?: string; // Added
  external_id?: any;
};
```

## Example Usage

### Creating a Cord

```typescript
import OZMapSDK from 'ozmapsdk';
// import { CreateCordDTO } from './Cord'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const newCordData = { // CreateCordDTO type assumed to be available
  parent: "baseBoxId123",
  name: "PatchCord-001",
  // external_id is optional
};

sdk.cord.create(newCordData).then((cord) => {
  console.log('Cord created:', cord);
});
```
Response example:
```json
{
  "_id": "cordIdXYZ",
  "name": "PatchCord-001",
  "parent": "baseBoxId123",
  "project": "projectIdAssociatedWithParent",
  "kind": "CORD",
  "connectors": ["connectorId1", "connectorId2"], // Example, these would be auto-generated
  "external_id": null,
  "createdAt": "2023-10-29T10:00:00.000Z",
  "updatedAt": "2023-10-29T10:00:00.000Z",
  "id": "cordIdXYZ"
}
```

### Updating a Cord

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateCordDTO } from './Cord'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateCordData = { // UpdateCordDTO type assumed to be available
  name: "PatchCord-001-Revised",
  external_id: "updatedExternalId",
};

sdk.cord.updateById('cordId', updateCordData).then(() => {
  console.log('Cord updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetching Cords

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.cord.find({ page: 1, limit: 10 }).then((pagination) => {
  console.log('Cords:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "cordIdXYZ",
      "name": "PatchCord-001",
      "parent": "baseBoxId123",
      "project": "projectIdAssociatedWithParent",
      "kind": "CORD",
      "connectors": ["connectorId1", "connectorId2"],
      "external_id": "updatedExternalId",
      "createdAt": "2023-10-29T10:00:00.000Z",
      "updatedAt": "2023-10-29T10:05:00.000Z", // Assuming it was updated
      "id": "cordIdXYZ"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a Cord by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.cord.findById('cordId').then((cord) => {
  console.log('Cord:', cord);
});
```
Response example:
```json
{
  "_id": "cordIdXYZ",
  "name": "PatchCord-001-Revised",
  "parent": "baseBoxId123",
  "project": "projectIdAssociatedWithParent",
  "kind": "CORD",
  "connectors": ["connectorIdNew1", "connectorIdNew2"], // Potentially updated
  "external_id": "updatedExternalId",
  "createdAt": "2023-10-29T10:00:00.000Z",
  "updatedAt": "2023-10-29T10:05:00.000Z",
  "id": "cordIdXYZ"
}
```

### Deleting a Cord

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.cord.deleteById('cordId').then(() => {
  console.log('Cord deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
```