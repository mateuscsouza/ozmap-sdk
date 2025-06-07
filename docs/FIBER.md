# Fiber Module

This document provides a concise guide to the Fiber module, focusing on the Fiber model and its Data Transfer Objects (DTOs) for update operations.

## Models

### Fiber

Defines the structure for fiber.

```typescript
type Fiber = {
  _id: string;
  id: string;
  kind: "FIBER"; // Simplified from NetworkConnectableKind
  name?: string; // From NetworkConnectable
  parent: string; // ID of the Cable
  project: string; // ID of the Project, from NetworkConnectable
  connectors: string[]; // Array of Connector IDs, from NetworkConnectable
  isDrop: boolean;
  fiberNumber: number;
  external_id?: any; // From BaseModel
  createdAt: string | Date; // From BaseModel
  updatedAt: string | Date; // From BaseModel
};
```

Note: Fibers are typically created and managed as part of a Cable, not directly. Therefore, a `CreateFiberDTO` is not provided.

### UpdateFiberDTO

Defines the structure for updating a fiber. (Note: Direct updates to fibers are limited).

```typescript
type UpdateFiberDTO = {
  name?: string; // The primary updatable field for a fiber directly
};
```

## Example Usage

### Updating a Fiber

```typescript
import OZMapSDK from 'ozmapsdk';
// import { UpdateFiberDTO } from './Fiber'; // DTO type assumed to be available

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

const updateFiberData = { // UpdateFiberDTO type assumed to be available
  name: "Fiber-01-Renamed", // Example: updating the name
};

sdk.fiber.updateById('fiberId', updateFiberData).then(() => {
  console.log('Fiber updated');
});
// The updateById method returns a Promise<void>.
// To confirm the update, you can re-fetch the entity or ensure the promise resolves successfully.
```

### Fetching Fibers

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.fiber.find({ page: 1, limit: 10 }).then((pagination) => {
  console.log('Fibers:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "fiberId123",
      "name": "Fiber-01-Renamed",
      "parent": "cableIdABC",
      "project": "projectIdXYZ",
      "kind": "FIBER",
      "connectors": ["connectorId1", "connectorId2"],
      "isDrop": false,
      "fiberNumber": 1,
      "external_id": null,
      "createdAt": "2023-10-30T12:00:00.000Z",
      "updatedAt": "2023-10-30T12:05:00.000Z",
      "id": "fiberId123"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a Fiber by ID

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.fiber.findById('fiberId').then((fiber) => {
  console.log('Fiber:', fiber);
});
```
Response example:
```json
{
  "_id": "fiberId123",
  "name": "Fiber-01-Renamed",
  "parent": "cableIdABC",
  "project": "projectIdXYZ",
  "kind": "FIBER",
  "connectors": ["connectorId1", "connectorId2"],
  "isDrop": false,
  "fiberNumber": 1,
  "external_id": "ext-fiber-001",
  "createdAt": "2023-10-30T12:00:00.000Z",
  "updatedAt": "2023-10-30T12:05:00.000Z",
  "id": "fiberId123"
}
```

### Deleting a Fiber

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.fiber.deleteById('fiberId').then(() => {
  console.log('Fiber deleted');
});
// The deleteById method returns a Promise<void>.
// To confirm the deletion, you can attempt to fetch the entity (expecting an error/null) or ensure the promise resolves successfully.
// Note: Direct deletion of a fiber might be restricted if it's part of a cable's defined structure.
```