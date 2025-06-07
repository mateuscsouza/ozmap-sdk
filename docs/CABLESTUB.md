# CableStub Module

This document provides a concise guide to the CableStub module, focusing on the CableStub model

## Models

### CableStub

Defines the structure for cableStubs.

```typescript
// import { CableStub } from './CableStub'; // Removed self-import

type CableStub = {
  kind: 'CableStub';
  project: string; // Simplified type
  name?: string; // Added
  coords: [number, number]; // Kept one
  cables?: string[]; // default: []
  pole?: string;
  observation?: string; // Added
};
```

Note: The CableStub model is generally managed as part of other entities or potentially read-only via a direct endpoint. Specific DTOs for direct creation or update, and examples for direct create, update, or delete operations, are not provided in this document as they are not typically performed on CableStubs directly.

## Example Usage

### Fetching CableStubs

```typescript
import OZMapSDK from 'ozmapsdk';

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.cableStub.find({ page: 1, limit: 10 }).then((pagination) => { // Corrected to sdk.cableStub
  console.log('CableStubs:', pagination);
});
```
Response example:
```json
{
  "total": 1,
  "count": 1,
  "rows": [
    {
      "_id": "cableStubId123",
      "kind": "CableStub",
      "project": "projectId456",
      "name": "CS-001",
      "coords": [-48.5001, -27.6001],
      "cables": ["cableId789"],
      "pole": "poleIdABC",
      "observation": "Stub near the old oak tree.",
      "tags": [],
      "createdAt": "2023-10-28T12:00:00.000Z",
      "updatedAt": "2023-10-28T12:00:00.000Z",
      "id": "cableStubId123"
    }
  ],
  "start": 0,
  "limit": 1
}
```

### Fetching a CableStub by ID

```typescript
import OZMapSDK from 'ozmapsdk';
// import cableStub from './CableStub'; // Removed incorrect import

const sdk = new OZMapSDK('ozmapURL', { apiKey: 'yourApiKey' });

sdk.cableStub.findById('cableStubId123').then((cableStubResult) => { // Corrected to sdk.cableStub and result variable
  console.log('CableStub:', cableStubResult);
});
```
Response example:
```json
{
  "_id": "cableStubId123",
  "kind": "CableStub",
  "project": "projectId456",
  "name": "CS-001",
  "coords": [-48.5001, -27.6001],
  "cables": ["cableId789"],
  "pole": "poleIdABC",
  "observation": "Stub near the old oak tree.",
  "tags": [],
  "createdAt": "2023-10-28T12:00:00.000Z",
  "updatedAt": "2023-10-28T12:00:00.000Z",
  "id": "cableStubId123"
}
```
